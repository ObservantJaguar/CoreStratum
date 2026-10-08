---
title: System Administrator
parent: Learning Paths
---

# Learning Path: System Administrator

A structured roadmap to become a System Administrator - the role that keeps infrastructure running. In a small organization a sysadmin is a generalist: servers, network basics, backups, mail, security basics and often hardware and access control. In larger companies the role narrows toward a specific domain.

## 1. Role overview

Read the [System Administrator role card](../roles/sysadmin.md): the job duties, the responsibility domains, and what is out of scope. The sysadmin path is the natural "zero point" from which many specialists grow (toward DevOps, SecOps or Network).

## 2. Foundations

- **Linux administration**: [installation, filesystem, users, permissions, services](../operating-systems/linux/index.md).
- **The shell**: [Bash scripting](../development/programming-languages/shell.md), cron, log analysis.
- **Networking fundamentals**: [TCP/IP, DNS, DHCP, TLS](../foundations/protocols/index.md), subnetting, routing basics.
- **Windows basics** (for mixed environments): user management, RDP, Active Directory concepts.

**Milestone:** you can install a Linux server, configure networking and users, and administer it remotely via SSH.

## 3. Core tools (by domain)

### Backups

- [Restic](../storage/backup/restic.md) and [BorgBackup](../storage/backup/borgbackup.md) - deduplicated encrypted backups.
- [ZFS/Btrfs snapshots](../storage/backup/zfs-snapshots.md) - instant filesystem snapshots.
- [Rclone](../storage/backup/rclone.md) - offsite copy.

### Mail

- [Postfix](../communications/email/postfix.md) + [Dovecot](../communications/email/dovecot.md) + [Rspamd](../communications/email/rspamd.md) - the classic mail trio.

### File sharing

- [Samba](../storage/network-filesystems/samba.md) - SMB shares for Windows clients.
- [NFS](../storage/network-filesystems/nfs.md) - Unix sharing.

### Virtualization

- [KVM](../virtualization/hypervisors/kvm.md) and [Proxmox VE](../containers/system-containers/proxmox-ve.md) - server virtualization.
- [LXC/LXD](../containers/system-containers/lxc.md) - lightweight isolated workloads.

### Monitoring

- [Zabbix](../observability/monitoring/zabbix.md) - host and service monitoring.
- [Grafana](../observability/alerting/grafana.md) - dashboards.
- [Netdata](../observability/monitoring/netdata.md) - quick real-time metrics.

### Networking basics

- [nftables/iptables](../networking/firewalls/nftables.md) - firewall rules.
- [WireGuard](../networking/vpn/wireguard.md) - VPN.
- [dnsmasq / BIND](../networking/dns/dnsmasq.md) - DNS/DHCP.

### Security basics

- [FreeIPA / Samba AD DC](../security/directory-services/freeipa.md) - accounts and domain.
- [Lynis](../security/hardening/lynis.md) - hardening audit.
- [Fail2ban / CrowdSec](../networking/intrusion-prevention/fail2ban.md) - basic protection.

## 4. Practice

Do these hands-on, in order:

1. [Docker Host with Traefik](../guides/docker-host-traefik.md) - host services in containers with TLS.
2. [Backup with restic and Borg](../guides/backup-restic-borg.md) - set up real backups and test a restore.
3. [Mail Server](../guides/mail-server.md) - Postfix + Dovecot + Rspamd.
4. [Nextcloud and CRM](../guides/nextcloud-crm.md) - file sharing and office tools.
5. Then the short [recipes](../guides/recipes/index.md) - SSH keys, firewall, LVM, cron, LUKS.

## 5. Typical vacancy stack

The recurring tools in sysadmin postings:

1. **Linux (Debian/Ubuntu or RHEL/Rocky)** - the platform.
2. **Bash** - scripting.
3. **Zabbix or similar** - monitoring.
4. **Nginx / Apache** - web serving.
5. **Postfix / Dovecot** - mail (in smaller companies).
6. **KVM / Proxmox** - virtualization.
7. **restic / Borg / rsync** - backups.

**You are job-ready when:** you can stand up a server from scratch, add users and shares, set up monitoring and backups, and find and fix a broken service from logs and `ps`/`netstat` without external help.

## Related

- [SysAdmin role card](../roles/sysadmin.md)
- [DevOps learning path](devops.md) (the natural next step)
- [Backup guide](../guides/backup-restic-borg.md)
- [Recipes](../guides/recipes/index.md)