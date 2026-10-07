---
title: Add a Firewall Rule (nftables/iptables)
parent: Recipes
grand_parent: Guides
---

# Add a Firewall Rule (nftables/iptables)

## Goal

Open a TCP/UDP port on a Linux host so external clients can reach a service.

## Task

Open port `8080/tcp` on a Linux server so a service listening on it becomes reachable from other hosts.

## Steps

1. Check which firewall framework is actually active (`nftables` is the default on modern distributions):

```bash
sudo nft list ruleset
sudo iptables -L -n
```

2. **nftables** - add the rule to the `input` chain:

```bash
sudo nft add rule inet filter input tcp dport 8080 accept
sudo nft list ruleset
```

Replace `inet filter` with your actual table/chain if it differs (check `nft list tables` and `nft list chain inet filter input`).

3. **iptables** - add the rule to the INPUT chain:

```bash
sudo iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
sudo iptables -L -n -v
```

4. Make the rules persistent so they survive a reboot.

On Debian/Ubuntu with `nftables`:

```bash
sudo nft list ruleset > /etc/nftables.conf
sudo systemctl enable --now nftables
```

With `iptables` + `netfilter-persistent`:

```bash
sudo apt install iptables-persistent
sudo netfilter-persistent save
```

## Verification

- Confirm the rule is present:

```bash
sudo nft list ruleset | grep 8080
```

- From another host, check the port is reachable:

```bash
nc -zv host.example.com 8080
```

## Gotchas

- **Rule order matters** - nftables/iptables stop at the first matching rule. If an earlier `DROP`/`REJECT` rule matches first, an extra `ACCEPT` rule added with `-A` (append) has no effect. Use `-I INPUT 1` / `nft insert` to put it ahead.
- **A higher-level firewall may sit on top** - `ufw` (Ubuntu) and `firewalld` (RHEL/Fedora) manage their own chains. If your rule "does not work", check `sudo ufw status` / `sudo firewall-cmd --state` and add the port there instead.
- **A host may run both nftables and iptables** - the legacy `iptables` backend and nftables can coexist. Look at what is actually in use (`iptables -L` vs `nft list ruleset`); `iptables-translate` converts legacy rules to nftables syntax if you need to consolidate.

## Related

- [Linux firewall fundamentals](../../security/hardening/index.md)