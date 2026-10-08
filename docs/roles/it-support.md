---
title: IT Support / Helpdesk
parent: IT Roles
---

# IT Support / Helpdesk

IT Support is the first line of the IT department: it receives user requests, keeps laptops and desktops working, manages accounts and access, and handles the physical side of the office. In a small business this role is often combined with a junior sysadmin who also watches the video surveillance and issues access badges. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Job duties

1. Handle user tickets and IT requests ([Tickets and request management](#tickets-and-request-management)).
2. Set up and maintain end-user hardware and operating systems ([End-user hardware and OS](#end-user-hardware-and-os)).
3. Manage user accounts, access and password policies ([Accounts and access](#accounts-and-access)).
4. Provide remote support and off-site access ([Remote access and VPN](#remote-access-and-vpn)).
5. Maintain physical security in a small business: badges and surveillance ([Physical security (small business)](#physical-security-small-business)).
6. Handle office networking basics and asset inventory ([Office networking (entry)](#office-networking-entry), [Tickets and request management](#tickets-and-request-management)).

## Responsibility domains

### Tickets and request management

- Helpdesk/ticketing and asset inventory: [GLPI](../engineering/eam/glpi.md), [NetBox](../engineering/eam/netbox.md), [Snipe-IT](../engineering/eam/snipe-it.md), [OCS Inventory](../engineering/eam/ocs-inventory.md).

### End-user hardware and OS

- Linux desktops: [Debian](../operating-systems/linux/distributions/debian.md), [Ubuntu Server/Desktop](../operating-systems/linux/distributions/ubuntu-server.md).
- Windows workstations in mixed environments: domain-joined clients via [Samba AD DC](../security/directory-services/samba4.md).
- Imaging and disk management: [LVM](../storage/block/lvm.md), [ZFS snapshots](../storage/backup/zfs-snapshots.md) for workstation backups.

### Accounts and access

- User accounts and password policy: [sudo](../security/hardening/sudo.md), [Samba AD DC](../security/directory-services/samba4.md), [FreeIPA](../security/directory-services/freeipa.md).
- Identity for self-service portals: [Keycloak](../security/authentication/keycloak.md).
- Secure remote shell access via SSH keys and the [SSH protocol](../foundations/protocols/index.md).

### Remote access and VPN

- Remote support tools: TeamViewer, AnyDesk (referenced as text).
- Off-site access: [OpenVPN](../networking/vpn/openvpn.md), [WireGuard](../networking/vpn/wireguard.md).

### Physical security (small business)

- Access badges and video surveillance (usually commercial systems, referenced as text) as a zone this role often owns in small companies.

### Office networking (entry)

- Simple switching and routing: [Open vSwitch](../networking/routing/openvswitch.md).
- Local DNS/DHCP for guests: [dnsmasq](../networking/dns/dnsmasq.md), [Kea](../networking/dhcp/kea.md).
- Baseline diagnostics: [tcpdump](../networking/diagnostics/tcpdump.md), [MTR](../networking/diagnostics/mtr.md).

## Out of scope

- Server and service infrastructure ownership (sysadmin).
- Production application code (developer).
- Network design, BGP/MPLS (network engineer).
- Security architecture and forensics (SecOps/InfoSec).

## Career path

- **IT Support → SysAdmin** — the classic progression: from user support to server administration.
- **IT Support → Network Engineer** — if the strongest part of the job was the network layer.
- **IT Support → DBA / DevOps** — depends on which advanced domain the person picks up.

## Related

- [System Administrator](sysadmin.md)
- [Network Engineer](network-engineer.md)