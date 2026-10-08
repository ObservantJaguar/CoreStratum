---
title: Network Engineer
parent: Learning Paths
---

# Learning Path: Network Engineer

A structured roadmap to become a Network Engineer. This role owns the connectivity layer: routing, switching, firewalls, VPNs and the physical/logical topology that everything else rides on. The path goes deep on protocols, then translates that theory into real Linux-based networking tools and appliances.

## 1. Role overview

Read the [Network Engineer role card](../roles/network-engineer.md) first: the responsibility domains, from LAN to WAN to edge. Key idea: networks are the substrate - a misconfigured route or firewall affects every other engineer in the building.

## 2. Foundations

- **Networking, deeply**: the OSI model, [TCP/IP, DNS, HTTP, TLS](../foundations/protocols/index.md), DHCP, ARP.
- **Addressing**: IPv4/IPv6, subnetting and VLSM, CIDR, NAT.
- **Switching**: VLANs, trunking, spanning tree, MAC tables.
- **Routing**: static versus dynamic protocols, default gateways, route selection.

**Milestone:** you can subnet a network by hand without a calculator, explain what happens on the wire when a host talks to a server in another subnet, and read a route table.

## 3. Core tools (by domain)

### Routing

- [FRRouting](../networking/routing/frr.md) - open-source routing suite (OSPF, BGP, RIP) on Linux.
- [VyOS](../networking/routing/vyos.md) - router/firewall distro with a CLI.

### Firewalls

- [nftables](../networking/firewalls/nftables.md) - the modern Linux firewall.
- [iptables](../networking/firewalls/iptables.md) - legacy Linux firewall (still on many boxes).
- **pfSense / OPNsense** - BSD-based gateway appliances (mention; no dedicated page yet).

### VPN

- [WireGuard](../networking/vpn/wireguard.md) - fast, modern site-to-site and road-warrior VPN.
- [OpenVPN](../networking/vpn/openvpn.md) - TLS-based VPN when you need more control.

### Diagnostics

- [Wireshark](../networking/diagnostics/wireshark.md) - packet capture and analysis.
- [tcpdump](../networking/diagnostics/tcpdump.md) - CLI packet capture for servers.
- [MTR](../networking/diagnostics/mtr.md) - combine ping and traceroute to find where packets drop.

### IPAM

- **NetBox** - IP address management and DCIM (mention; no dedicated page yet).

## 4. Practice

Do these hands-on, in order:

1. [Docker Host with Traefik](../guides/docker-host-traefik.md) - see load balancing and reverse-proxy routing in practice (DNS + TLS + path routing).
2. [Recipes](../guides/recipes/index.md) - [firewall rule](../guides/recipes/firewall-rule.md), [DNS diagnostics](../guides/recipes/dns-diagnostics.md): the daily toolkit.
3. Build a real Linux router: two subnets, static routes or FRRouting, a NAT rule, and verify the path with Wireshark/tcpdump.

## 5. Typical vacancy stack

The recurring tools in network-engineer postings:

1. **Cisco IOS or FRRouting** - routing/switching fundamentals.
2. **MikroTik RouterOS** - very common in small/medium networks.
3. **pfSense or OPNsense** - firewall and gateway appliances.
4. **Wireshark** - packet analysis.
5. **WireGuard / OpenVPN** - VPN.
6. **VLAN + subnetting discipline** - the skill, more than any tool.

**You are job-ready when:** you can design a small routed network, configure inter-VLAN routing and a firewall, set up site-to-site VPN, and isolate a connectivity fault with a packet capture - without stepping through every command from a tutorial.

## Related

- [Network Engineer role card](../roles/network-engineer.md)
- [Cloud Engineer role card](../roles/cloud-engineer.md) (adjacent - networks in the cloud)
- [SysAdmin learning path](sysadmin.md)
- [Guides](../guides/index.md)
- [Recipes](../guides/recipes/index.md)