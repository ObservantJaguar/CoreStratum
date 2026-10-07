---
title: Generate and Trust a Self-Signed Certificate
parent: Recipes
grand_parent: Guides
---

# Generate and Trust a Self-Signed Certificate

## Goal

Create a locally trusted HTTPS certificate for a dev / intranet service with `openssl`.

## Task

Produce a valid pair of `cert.pem` / `key.pem` for `host.local` and make clients trust it as their CA.

## Steps

1. Generate a self-signed certificate and key (CN plus Subject Alternative Names for the hostnames/IPs it will serve):

```bash
openssl req -x509 -newkey rsa:2048 -nodes -days 365 -keyout key.pem -out cert.pem -subj "/CN=host.local" -addext "subjectAltName=DNS:host.local,DNS:host,IP:192.168.1.10" -addext "keyUsage=digitalSignature,keyEncipherment" -addext "extendedKeyUsage=serverAuth"
```

2. Distribute `cert.pem` as a CA to every client that should trust it.

3. Trust the CA:

On Debian/Ubuntu:

```bash
sudo cp cert.pem /usr/local/share/ca-certificates/host-local.crt
sudo update-ca-certificates
```

On RHEL/Fedora:

```bash
sudo trust anchor cert.pem
sudo update-ca-trust
```

4. Point your server (nginx, apache, vault, or dev proxy) at `cert.pem` and `key.pem`.

## Verification

- The server presents the cert and it chains to your local CA:

```bash
openssl s_client -connect host.local:443 -servername host.local < /dev/null
```

Look for the `subject` and `issuer`, and no `verify error` when your CA is trusted.

- A `curl` to the server succeeds against its own trust store:

```bash
curl -v https://host.local
```

returns HTTP 200 with the certificate chain signed by your trusted CA.

## Gotchas

- **San is mandatory for modern browsers** - Chrome/Firefox reject a cert whose hostname is not listed in `subjectAltName`, even if `CN` matches. Always add `-addext subjectAltName=...` with the exact hostnames/IPs.
- **CN is legacy** - modern clients ignore the CN for name matching; rely on SAN only.
- **Include `keyUsage` / `extendedKeyUsage`** - without `serverAuth` and the right key usage, TLS servers may refuse the cert or clients reject it for lack of serverAuth.
- **Clients check the validity dates** - `-days 365` and machine clock skew older/newer can make a cert "not yet valid" or "expired". Regenerate if the date is off.
- **Revocation** - there is no sanitation; if the key leaks, distribute a new cert and remove the old one from trusting clients.

## Related

- [Public key infrastructure](../../security/cryptography/index.md)
- [TLS in depth](../../security/cryptography/gnupg.md)