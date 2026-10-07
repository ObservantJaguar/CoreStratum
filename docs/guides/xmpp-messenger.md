---
grand_parent: Practice
title: XMPP Messenger
parent: Guides
---

# XMPP Messenger

## Goal

A self-hosted **XMPP (Jabber)** messaging server for a small organization: instant messaging, presence, file transfers, and **audio/video calls via Jingle** — the open VoIP-style extension of XMPP. The stack is **ejabberd** (server, written in Erlang), **coturn** (TURN for calls) and the best clients for each platform: **Conversations** (Android), **Gajim** or **Dino** (Linux), **Monal** (iOS/macOS), **Gajim** (Windows).

XMPP is the lean, fully decentralized alternative to Matrix: it is lightweight, battle-tested, and — with Jingle — genuinely supports voice and video, even though the client ecosystem is not as polished as Element's.

## Scope and out of scope

**In scope:**
- ejabberd server deployment (Docker, behind the Traefik foundation layer)
- Domain configuration (`example.com` as the XMPP domain)
- TLS via Let's Encrypt
- Jingle calls with coturn (STUN/TURN)
- Client setup (Conversations, Gajim, Dino, Monal)
- Basic anti-abuse settings (registration policy, MAM archiving)

**Out of scope:**
- Group video conferences (XMPP has no comparable SFU ecosystem yet — mention and link to Matrix guide if the team needs it)
- SIP/PSTN integration (that's the [IP Telephony](ip-telephony.md) guide)
- Multi-domain federation tuning

## Protocol background

XMPP itself only handles **signaling**: who is calling whom, and under what parameters. The media itself flows outside the server over **RTP**, exactly like VoIP. The relevant Jingle extensions:

| XEP | Purpose |
|---|---|
| XEP-0166 | Jingle — session negotiation |
| XEP-0167 | Jingle RTP Sessions — audio/video transport |
| XEP-0176 | Jingle ICE-UDP — NAT traversal |
| XEP-0343 | Jingle WebRTC SDP — interop with browser clients |

This is why the architecture below looks a lot like the [Matrix Messenger](matrix-messenger.md) and [IP Telephony](ip-telephony.md) ones: an XMPP server for signaling plus coturn for media.

## Architecture

```
  Conversations / Gajim / Dino / Monal
        РІвЂќвЂљ   (XMPP text + presence over TLS 5222)
        РІвЂќвЂљ
        РІвЂќвЂљ   (Jingle media over RTP/UDP, outside the XMPP server)
        РІвЂќСљРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂ“С” coturn РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂ“С” other user (if behind NAT)
        РІвЂќвЂљ
  РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂ“СРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’
  РІвЂќвЂљ  ejabberd  (example.com)        РІвЂќвЂљ
  РІвЂќвЂљ   РІвЂќСљРІвЂќР‚РІвЂќР‚ TLS 5222 (client)         РІвЂќвЂљ
  РІвЂќвЂљ   РІвЂќСљРІвЂќР‚РІвЂќР‚ 5269 (s2s federation)     РІвЂќвЂљ
  РІвЂќвЂљ   РІвЂќСљРІвЂќР‚РІвЂќР‚ MAM (archiving)           РІвЂќвЂљ
  РІвЂќвЂљ   РІвЂќвЂќРІвЂќР‚РІвЂќР‚ SQLite/PostgreSQL store   РІвЂќвЂљ
  РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ
```

## Roadmap

### Stage 1 — Foundation and DNS

- [ ] Follow the [Docker Host with Traefik](docker-host-traefik.md) guide if not done
- [ ] DNS records: `example.com` (XMPP domain) and `turn.example.com` for TURN

```text
example.com.      A  203.0.113.20
conference.example.com.  A  203.0.113.20     (MUC)
turn.example.com. A  203.0.113.20
```

XMPP clients discover the server via DNS SRV records:

```text
_xmpp-client._tcp.example.com.  SRV  5 0 5222 example.com.
_xmpp-server._tcp.example.com.  SRV  5 0 5269 example.com.
```

### Stage 2 — Deploy ejabberd

Create `/opt/containers/xmpp/docker-compose.yml`:

```yaml
services:
  ejabberd:
    image: ejabberd/ecs:latest
    container_name: ejabberd
    restart: unless-stopped
    ports:
      - "5222:5222"    # client-to-server
      - "5269:5269"    # server-to-server
      - "5443:5443"    # web admin (HTTPS)
      - "5280:5280"    # HTTP upload, web client access
      - "5281:5281"    # HTTP upload (TLS)
    volumes:
      - ./conf:/opt/ejabberd/conf
      - ./data:/opt/ejabberd/data
    environment:
      - ERLANG_NODE=ejabberd@localhost
      - EJABBERD_ADMINS=admin@example.com
      - XMPP_DOMAIN=example.com
```

- [ ] First start generates default config in `./conf/ejabberd.yml`
- [ ] Set an admin account

### Stage 3 — Configure the domain and TLS

- [ ] Set `hosts: [example.com]`
- [ ] Enable Let's Encrypt via the ejabberd built-in ACME support, or mount certs from the Traefik `letsencrypt` directory into the container
- [ ] Ensure `certfiles` points to the fullchain and key
- [ ] Restart and check ejabberd logs for certificate loading

If you prefer to reuse the Traefik certificate store, mount:

```yaml
volumes:
  - "/opt/containers/traefik/letsencrypt:/certs:ro"
```

and configure `certfiles: /certs/**/*.pem`.

### Stage 4 — Create users

- [ ] Register the first admin (web admin at `https://example.com:5443` or `ejabberdctl`)
- [ ] Create regular users

```bash
docker exec -it ejabberd ejabberdctl register admin example.com 'StrongPass123'
docker exec -it ejabberd ejabberdctl register alice example.com 'Pass2'
```

### Stage 5 — Enable archiving (MAM) and useful modules

- [ ] Enable **MAM** (message archive) so history survives client switches
- [ ] Enable **HTTP Upload** for file sharing
- [ ] Enable **MUC** (group chats): `mod_muc` with `conference.example.com`

Example config additions (`conf/ejabberd.yml`):

```yaml
modules:
  mod_mam:
    default: always
  mod_http_upload:
    hosts:
      - "upload.example.com"
    dir: "/opt/ejabberd/upload"
  mod_muc:
    host: "conference.example.com"
    access: muc_online
```

### Stage 6 — coturn for Jingle calls

Jingle calls need STUN/TURN for NAT traversal, exactly like Matrix or SIP. Deploy coturn:

```yaml
services:
  coturn:
    image: coturn/coturn:latest
    restart: unless-stopped
    command: >
      -n --log-file=stdout
      --lt-cred-mech --fingerprint --no-multicast-peers
      --realm=example.com
      --static-auth-secret=CHANGE_ME_TURN_SECRET
      --listening-port=3478
      --min-port=49152 --max-port=65535
    ports:
      - "3478:3478/udp"
      - "49152-65535:49152-65535/udp"
```

- [ ] Open UDP 3478 and 49152РІР‚вЂњ65535 on the firewall
- [ ] In clients, configure the STUN/TURN server (`turn:turn.example.com:3478?transport=udp`) with the shared secret or long-term credentials
- [ ] Test a call between two devices on different networks

### Stage 7 — Client setup

| Client | Platform | Notes |
|---|---|---|
| [Conversations](https://conversations.im) | Android | Best Android XMPP client, OMEMO e2e encryption, calls |
| [Gajim](https://gajim.org) | Linux/Windows | Full-featured, plugins, calls via Jingle |
| [Dino](https://dino.im) | Linux (GNOME) | Simple, clean, calls |
| [Monal](https://monal-im.org) | iOS/macOS | The main iOS option, OMEMO, calls |

- [ ] Set your own server: `example.com` (discovered via SRV) or explicitly `xmpp://example.com`
- [ ] Enable OMEMO encryption (Conversations/Gajim) for E2E on direct messages
- [ ] Test file upload and group chat

### Stage 8 — Backup

- [ ] Back up the ejabberd data directory (MAM archive, users, roster)
- [ ] Include the config and certs
- [ ] Wire into the [Backup with restic and Borg](backup-restic-borg.md) guide

## Verification

- [ ] `dig SRV _xmpp-client._tcp.example.com` resolves
- [ ] `openssl s_client -connect example.com:5222 -starttls xmpp` shows a valid certificate
- [ ] Two users exchange direct messages and both see presence
- [ ] A group chat (MUC) works at `conference.example.com`
- [ ] A **voice call** between two devices connects (check TURN usage in coturn logs)
- [ ] History is restored after reinstall (MAM works)

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Clients can't connect | DNS SRV missing or wrong port | Verify `_xmpp-client._tcp` SRV; check firewall 5222 |
| Certificate warnings | Cert not matching `example.com` or self-signed | Mount a valid Let's Encrypt cert; check `certfiles` |
| Calls fail | coturn not configured in client | Configure STUN/TURN in client settings; open UDP range |
| Messages lost on reinstall | MAM off or data directory not backed up | Enable `mod_mam`; include `data/` in backup |
| Groups don't work | `mod_muc` not enabled | Add `mod_muc` with `conference.example.com` |

### XMPP vs Matrix — which one for your team?

- **Choose XMPP** if you value leanness, total decentralization and a simple protocol, and your team mainly needs text + occasional 1:1 calls.
- **Choose Matrix** ([guide](matrix-messenger.md)) if group voice/video calls and the richest clients are a hard requirement.

## Related pages

- [ejabberd](../communications/messaging/ejabberd.md)
- [Prosody (alternative server)](../communications/messaging/prosody.md)
- [Conversations](../communications/messaging/conversations.md)
- [coturn](../communications/messaging/coturn.md)
- [Matrix Messenger guide (for group calls)](matrix-messenger.md)
- [IP Telephony guide (SIP alternative)](ip-telephony.md)