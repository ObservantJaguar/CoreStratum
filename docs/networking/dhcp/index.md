---
title: DHCP
parent: Networking
grand_parent: Tools
---

# DHCP

The Dynamic Host Configuration Protocol (DHCP) automatically assigns IP addresses and network configuration to hosts on a network. This category covers DHCPv4/v6 servers, failover, static reservations, integration with DNS for dynamic updates, and the PXE/network boot provisioning that depends on DHCP to bootstrap diskless clients.

- [ISC DHCP](isc-dhcp.md) — the classic reference DHCP server and relay implementation.
- [Kea](kea.md) — modern, high-performance and API-driven DHCP suite.

[dnsmasq](../dns/dnsmasq.md) also includes a simple DHCP server and is documented in the DNS category. Network boot (PXE) provisioning typically pairs a DHCP server with a TFTP/HTTP boot server such as dnsmasq, ISC DHCP with a PXE boot image, or a dedicated provisioning platform.