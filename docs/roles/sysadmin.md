---
title: System Administrator
parent: IT Roles
---

# System Administrator

The System Administrator keeps the infrastructure running day to day. In a small organization this role is famously broad: the same person covers servers, network basics, backups, mail, user accounts, and often hardware, surveillance and access badges. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Responsibility domains

### Backups and recovery

- Encrypted, deduplicated backups: [restic](../storage/backup/restic.md), [BorgBackup](../storage/backup/borgbackup.md).
- Snapshot workflows: [ZFS snapshots](../storage/backup/zfs-snapshots.md), [Timeshift](../storage/backup/timeshift.md), [Snapper](../storage/backup/snapper.md).
- Offsite transport: [Rclone](../storage/backup/rclone.md), rsync.
- Large-scale network backup: [Bacula](../storage/backup/bacula.md), [UrBackup](../storage/backup/urbackup.md).
- Protocol: [NFS](../foundations/protocols/index.md), [SMB/CIFS](../foundations/protocols/index.md).

### Mail infrastructure

- MTA: [Postfix](../communications/email/postfix.md), [Exim](../communications/email/exim.md).
- Delivery (IMAP/POP): [Dovecot](../communications/email/dovecot.md).
- Filtering: [Rspamd](../communications/email/rspamd.md), [ClamAV](../communications/email/clamav.md).
- Webmail: [Roundcube](../communications/email/roundcube.md), [RainLoop](../communications/email/rainloop.md).
- Protocols: [SMTP, IMAP, POP3](../foundations/protocols/index.md).

### File services

- [Samba / SMB](../storage/network-filesystems/samba.md), [NFS](../storage/network-filesystems/nfs.md), [SSHFS](../storage/network-filesystems/sshfs.md).

### Virtualization

- Server: [KVM](../virtualization/hypervisors/kvm.md), [Proxmox VE](../containers/system-containers/proxmox-ve.md), [bhyve](../virtualization/hypervisors/bhyve.md).
- Hosted: [VirtualBox](../virtualization/hosted/virtualbox.md), [Multipass](../virtualization/hosted/multipass.md).
- Isolated workloads: [LXC/LXD](../containers/system-containers/lxc.md), [FreeBSD jails](../virtualization/isolation/freebsd-jails.md).

### Monitoring and observability

- Monitoring: [Zabbix](../observability/monitoring/zabbix.md), [Netdata](../observability/monitoring/netdata.md), [Prometheus](../observability/monitoring/prometheus.md).
- Dashboards: [Grafana](../observability/alerting/grafana.md).
- Alerts: [Alertmanager](../observability/alerting/alertmanager.md).
- Logs: [Loki](../observability/logging/loki.md), [Graylog](../observability/logging/graylog.md), [ELK](../observability/logging/elasticsearch.md).

### Networking basics

- Firewalls: [nftables](../networking/firewalls/nftables.md), [iptables](../networking/firewalls/iptables.md), [pfSense/OPNsense](../networking/firewalls/index.md), [OpenVPN/WireGuard](../networking/vpn/wireguard.md).
- DNS/DHCP: [BIND](../networking/dns/bind.md), [dnsmasq](../networking/dns/dnsmasq.md), [Kea](../networking/dhcp/kea.md).
- Diagnostics: [Wireshark](../networking/diagnostics/wireshark.md), [tcpdump](../networking/diagnostics/tcpdump.md), [MTR](../networking/diagnostics/mtr.md).
- Protocols: [TCP/IP, DNS, DHCP, TLS](../foundations/protocols/index.md).

### Security basics

- Account/directory: [FreeIPA](../security/directory-services/freeipa.md), [OpenLDAP](../security/directory-services/index.md), [Samba AD DC](../security/directory-services/samba4.md).
- Hardening: [Lynis](../security/hardening/lynis.md), [SELinux](../security/hardening/selinux.md), [AppArmor](../security/hardening/apparmor.md).
- Remote protection: [Fail2ban](../networking/intrusion-prevention/fail2ban.md), [CrowdSec](../networking/intrusion-prevention/crowdsec.md).
- Access: [sudo](../security/hardening/sudo.md), [SSH keys](../guides/recipes/ssh-key-auth.md).

### Automation (entry)

- Configuration: [Ansible](../automation/configuration-management/ansible.md).
- Scripting: Bash, cron, rsync.
- Provisioning: [Cloud-Init](../automation/iac/cloud-init.md), [Vagrant](../automation/provisioning/vagrant.md).

## Out of scope

- Writing application features (developer).
- Production pipeline ownership (DevOps).
- Long-term capacity and SLO engineering (SRE).
- Formal security architecture and threat modelling (SecOps).
- Deep network design, BGP/MPLS (Network Engineer).

## Career path

- **SysAdmin → DevOps** — add IaC, CI/CD and containers.
- **SysAdmin → SecOps** — specialize in hardening, audit, incident response.
- **SysAdmin → SRE** — adopt reliability metrics and automation at scale.

## Related

- [DevOps Engineer](devops.md)
- [SRE](sre.md)
- [IT Support / Helpdesk](it-support.md)