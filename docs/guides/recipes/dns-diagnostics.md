---
title: Diagnose DNS Resolution Problems
parent: Recipes
grand_parent: Guides
---

# Diagnose DNS Resolution Problems

## Goal

Find out why a hostname does not resolve, and where in the resolution path the failure sits.

## Task

Diagnose why `example.com` does not resolve on a Linux workstation.

## Steps

1. Ask a known-good public resolver directly, bypassing your local setup:

```bash
dig @1.1.1.1 example.com
```

Or interactively:

```bash
nslookup example.com 1.1.1.1
```

2. Trace the full resolution path to find where it stops:

```bash
dig +trace example.com
```

3. Query the specific record type you care about:

```bash
host -t A example.com
```

4. Check what the system is actually configured to use:

```bash
cat /etc/resolv.conf
systemd-resolve --status        # older
resolvectl status                # newer
```

5. If a local stub resolver is involved, test in the clear to isolate it:

```bash
resolvectl query example.com
```

## Verification

- A plain query resolves:

```bash
dig example.com +short
```

returns the expected IP address (not empty, not `SERVFAIL`/`NXDOMAIN`).

## Gotchas

- **Local resolver cache can serve stale/negative answers** - `systemd-resolved`, `NetworkManager`, `dnsmasq` or `unbound` may cache a bad result. Flush with `resolvectl flush-caches` (or `sudo systemd-resolve --flush-caches`) before re-testing.
- **split-DNS / VPN** - a VPN or company DNS zone can route a name to a non-public, internal answer that only works on the VPN. Compare `dig @PUBLIC example.com` with the configured-resolver result.
- **TTL caching** - recent changes to a zone can take up to the old TTL (often minutes to hours) to propagate; do not conclude a record is missing within the TTL window.
- **IPv6 / AAAA without IPv6** - a host may return only `AAAA` records, or an A record may be absent while AAAA exists and your network has no IPv6. Always check both `A` and `AAAA` (or use `getent ahosts`).

## Related

- [DNS in depth](../../networking/dns/index.md)
- [Network diagnostics](../../storage/backup/index.md)