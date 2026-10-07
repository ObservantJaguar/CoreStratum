---
grand_parent: Practice
title: Mail Server
parent: Guides
---

# Mail Server

## Goal

A self-hosted mail server for a small organization: users receive mail on their own domain and send mail that actually lands in the recipient's inbox (not spam). The stack is **Postfix** (MTA), **Dovecot** (IMAP/POP3), **Rspamd** (spam filtering) and **Roundcube** (webmail), with full **SPF, DKIM and DMARC** records, encrypted connections and optional antivirus.

This is honest scope: a mail server is the hardest self-hosted service to run well. The reward is full control of your mail data.

## Scope and out of scope

**In scope:**
- Postfix SMTP server (send and receive for your domain)
- Dovecot IMAP server with TLS, Maildir storage
- Rspamd spam filtering with learning (Bayes)
- SPF, DKIM, DMARC records and rDNS (PTR) setup
- Roundcube webmail as a user interface
- Backup and restore of mailboxes

**Out of scope:**
- Calendars/CardDAV (consider adding Nextcloud or SOGo)
- Large-scale anti-abuse tooling (this is for a small domain)
- Full-text search indexing (possible later with Dovecot FTS)

## Prerequisites

- A dedicated (or virtual) server with a public, static IPv4 (and IPv6 if possible)
- A domain you control, with DNS provider access
- Forward and reverse DNS (PTR) for the mail hostname
- Ports 25 (SMTP), 587 (submission), 143/993 (IMAP), 80/443 (webmail)
- The server must not be on a residential/blocked IP range; check your provider's reputation policies

**Critical DNS facts to confirm first:**

```text
Your server hostname:  mail.example.com
A record:              mail.example.com -> 203.0.113.10
PTR record:            10.113.0.203.in-addr.arpa -> mail.example.com
MX record:             example.com MX 10 mail.example.com
```

If you cannot set PTR (some VPS providers allow it only via support request), arrange it with the provider **before** going further — mail will often be rejected without matching forward/reverse DNS.

## Architecture

```
                    +----------------------------------------------+
 Internet --------->|  Postfix  (port 25/587, TLS)                |
     SMTP           |    |                                        |
                    |    +-------> Dovecot  (IMAP 143/993)   <+   |
                    |    |            \-- Maildir            |   |
                    |    +-------> Rspamd  (spam filter)     |   |
                    |    |                                   |   |
                    |    +-------> Roundcube (webmail, https)|   |
                    +----------------------------------------------+
                                                                   |
                                                        user (Thunderbird, phone)
   DNS: MX + SPF (TXT) + DKIM (TXT) + DMARC (TXT) + PTR
```

## Roadmap

### Stage 1 — DNS: MX, SPF, and host naming

- [ ] Choose the mail hostname (`mail.example.com`)
- [ ] Set A/AAAA and arrange the PTR record with the provider
- [ ] Add the MX record for the domain
- [ ] Publish the SPF record allowing your server

```text
MX:    example.com.  IN  MX  10  mail.example.com.
A:     mail.example.com.  A  203.0.113.10
TXT:   @  IN  TXT  "v=spf1 a mx ip4:203.0.113.10 -all"
```

Wait for DNS to propagate before testing sending.

### Stage 2 — Install the stack

On Debian/Ubuntu:

```bash
sudo apt update
sudo apt install -y postfix dovecot-imapd dovecot-lmtpd rspamd roundcube
```

During Postfix installation choose **"Internet Site"** and set `mail.example.com` as the mail name.

- [ ] Verify all services start: `postfix`, `dovecot`, `rspamd`
- [ ] Confirm `systemctl status` for all three

### Stage 3 — Create mail users

- [ ] Create system users (or a virtual user table) for the mailboxes
- [ ] For a small org, system users are simplest

```bash
sudo useradd --create-home --shell /usr/sbin/nologin alice
sudo passwd alice
```

### Stage 4 — Configure Dovecot (IMAP + LMTP)

- [ ] Point Dovecot to Maildir (or mdbox) storage
- [ ] Enable LMTP so Postfix hands incoming mail to Dovecot
- [ ] Force TLS for IMAP connections

Example `/etc/dovecot/conf.d/10-mail.conf`:

```ini
mail_location = maildir:~/Maildir
```

Enable `imap` and `lmtp` in `10-master.conf` (listen on the local socket for LMTP):

```text
service lmtp { unix_listener /var/spool/postfix/private/dovecot-lmtp { mode = 0660 user = postfix group = postfix } }
```

TLS (`10-ssl.conf`):

```ini
ssl = required
ssl_cert = </etc/letsencrypt/live/mail.example.com/fullchain.pem
ssl_key  = </etc/letsencrypt/live/mail.example.com/privkey.pem
```

Restart Dovecot after each change.

### Stage 5 — Configure Postfix

- [ ] Set the hostname and mydestination
- [ ] Route incoming mail to Dovecot via LMTP
- [ ] Enable submission (port 587) with SASL auth
- [ ] Enable DKIM signing (OpenDKIM or in Rspamd)

Minimal `/etc/postfix/main.cf` additions:

```ini
myhostname = mail.example.com
mydomain = example.com
myorigin = $mydomain
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
# Virtual users handled via Dovecot LMTP
virtual_transport = lmtp:unix:private/dovecot-lmtp
# Submission (port 587) with auth
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
```

DKIM with Rspamd:

```ini
# in main.cf
milter_default_action = accept
milter_protocol = 2
smtpd_milters = local:rspamd/rspamd.sock
non_smtpd_milters = local:rspamd/rspamd.sock
```

### Stage 6 — DKIM key and DNS records

- [ ] Generate a DKIM key pair
- [ ] Publish the public key as a TXT record
- [ ] Test with `opendkim-testkey` or `rspamadm dkim` (depending on tool)

With Rspamd (simplest for this stack):

```bash
sudo mkdir -p /etc/rspamd/local.d/dkim
sudo rspamadm dkim_keygen -b 2048 -s mail -d example.com
```

Place the resulting private key in a configured path and publish:

```text
mail._domainkey.example.com. IN TXT "v=DKIM1; k=rsa; p=<public key here>"
```

### Stage 7 — SPF, DMARC

- [ ] Confirm SPF record is published and correct
- [ ] Add a DMARC record (start with `p=none`, then tighten after monitoring)
- [ ] (Optional) add a `_dmarc` reporting address

```text
_dmarc.example.com. IN TXT "v=DMARC1; p=none; rua=mailto:dmarc@example.com"
```

### Stage 8 — TLS certificates

- [ ] Obtain a certificate for `mail.example.com` (certbot or the Docker/Traefik layer)
- [ ] Install it in Postfix, Dovecot and webmail
- [ ] Set up renewal and restart services after renewal

**Note:** If you use the [Docker Host with Traefik](docker-host-traefik.md) guide from the foundation layer, the certificate for Roundcube comes automatically; Postfix/Dovecot still need their own copy for SMTP/IMAP.

### Stage 9 — Webmail (Roundcube)

- [ ] Configure Roundcube to connect to Dovecot IMAP and SMTP
- [ ] Publish it behind TLS (Traefik or Nginx)
- [ ] Test login with `alice@example.com`

### Stage 10 — Spam filtering and learning

- [ ] Verify Rspamd is receiving and scanning mail
- [ ] Teach Rspamd about good/bad mail (web UI or `learn_spam`/`learn_ham`)
- [ ] Set a sensible action for high-scoring mail (quarantine or add header; avoid hard-rejecting on the first week)

---

## Verification

- [ ] `dig MX example.com`, `dig TXT @ _dmarc.example.com` show the records
- [ ] `host mail.example.com` and PTR match
- [ ] Send mail to a personal external address and confirm delivery (not spam)
- [ ] Receive a reply and confirm it lands in the mailbox
- [ ] `rspamadm stat` shows messages scanned and statistics
- [ ] `openssl s_client -connect mail.example.com:993` shows a valid certificate
- [ ] A test via `swaks --to alice@example.com --server mail.example.com` (submission plus auth) succeeds

### Online tools for final check

- `https://www.mail-tester.com` — send a test mail, get a score
- `https://dnschecker.org` — verify TXT records propagation
- `https://www.mailhardener.com/tools/spf-validator` — validate SPF

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Mail from your server goes to spam | No/mismatched rDNS, no SPF, missing DKIM | Fix PTR, publish SPF, ensure DKIM signs outgoing mail |
| Can't receive mail | MX wrong or port 25 blocked | Check `dig MX`, firewall, provider policy on port 25 |
| Auth fails on 587 | SASL not wired | Verify `smtpd_sasl` options and Dovecot auth socket path |
| Rspamd not scanning | milter socket path mismatch | Confirm `smtpd_milters` socket matches Rspamd's actual socket |
| Certificate renewal breaks IMAP | Postfix/Dovecot not reloaded | Add `--deploy-hook` in certbot to reload postfix+dovecot |
| Port 25 blocked by ISP | Hosting provider policy | Move to a provider allowing SMTP, or use a relay (see note below) |

### When to use a relay

If your ISP/VPS provider blocks outbound port 25, or you only send transactional mail, use a **relay** (for example a mailer service with SMTP API). The guide then stays identical except Postfix is told `relayhost = smtp.provider.example:587` and to send via submission with credentials.

## Related pages

- [Postfix](../communications/email/postfix.md)
- [Dovecot](../communications/email/dovecot.md)
- [Rspamd](../communications/email/rspamd.md)
- [Roundcube](../communications/email/roundcube.md)
- [ClamAV (optional antivirus)](../communications/email/clamav.md)
- [Restic and Borg (mailbox backup)](backup-restic-borg.md)