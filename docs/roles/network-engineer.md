---
title: Network Engineer
parent: IT Roles
---

# Network Engineer

The Network Engineer designs, implements and operates the network: routers, switches, firewalls, VPNs, load balancers and the protocols that move traffic between systems. In small companies this role is usually folded into the sysadmin position until the network grows complex enough to justify a specialist. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Responsibility domains

### Routing and switching

- Routing suites: [FRRouting](../networking/routing/frr.md), [VyOS](../networking/routing/vyos.md), [BIRD](../networking/routing/bird.md).
- Software-defined switching: [Open vSwitch](../networking/routing/openvswitch.md), [ONOS](../networking/switching/onos.md), [Faucet](../networking/switching/faucet.md).
- Protocols: [OSPF, BGP, VLANs, STP](../foundations/protocols/index.md).

### Firewalls

- Host firewalls: [nftables](../networking/firewalls/nftables.md), [iptables](../networking/firewalls/iptables.md), [pf](../networking/firewalls/pf.md).
- Appliance/software firewalls: [pfSense/OPNsense](../networking/firewalls/index.md).

### VPN and remote access

- WireGuard: [WireGuard](../networking/vpn/wireguard.md).
- TLS VPN: [OpenVPN](../networking/vpn/openvpn.md).
- Mesh overlays: [Tailscale](../networking/vpn/tailscale.md), [ZeroTier](../networking/vpn/zerotier.md).

### Load balancing

- Layer 4: [HAProxy](../communications/web/haproxy.md), [Keepalived/VIP](../networking/load-balancing/keepalived.md).
- Layer 7: [Envoy](../networking/load-balancing/envoy.md), [Traefik](../networking/load-balancing/traefik.md), [Varnish](../networking/load-balancing/varnish.md).

### DHCP and DNS infrastructure

- DNS: [BIND](../networking/dns/bind.md), [dnsmasq](../networking/dns/dnsmasq.md), [CoreDNS](../networking/dns/coredns.md), [Unbound](../networking/dns/unbound.md), [PowerDNS](../networking/dns/powerdns.md).
- DHCP: [Kea](../networking/dhcp/kea.md), [ISC DHCP](../networking/dhcp/isc-dhcp.md).

### Diagnostics and troubleshooting

- Packet analysis: [Wireshark](../networking/diagnostics/wireshark.md), [tcpdump](../networking/diagnostics/tcpdump.md), [netcat](../networking/diagnostics/netcat.md).
- Path tracing: [MTR](../networking/diagnostics/mtr.md).

### Network observability and IPAM

- Network monitoring and asset registry: [NetBox](../engineering/eam/netbox.md), [GLPI](../engineering/eam/glpi.md).
- Protocol-level metrics: [Prometheus via SNMP exporters](../observability/monitoring/prometheus.md).

## Out of scope

- Server operating systems and applications (sysadmin).
- Application security scanning (SecOps/DevSecOps).
- Developing software (developer).
- Content-level WAF rules and DDoS application hardening (often shared with SecOps).

## Career path

- **SysAdmin → Network Engineer** — sysadmins who specialize in the network layer.
- **Network Engineer → Cloud Engineer** — when the network moves into cloud VPCs, load balancers and Cloud WAN.
- **Network Engineer ↔ SecOps** — firewalls and segmentation boundaries are shared territory.

## Related

- [System Administrator](sysadmin.md)
- [Cloud Engineer](cloud-engineer.md)
- [SecOps / Security Engineer](secops.md)