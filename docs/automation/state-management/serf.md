---
title: Serf
parent: State Management
---

# Serf

Serf is a decentralized cluster membership, failure detection, and gossip protocol tool from HashiCorp. It meets the needs of scaling into large clusters by maintaining node membership and propagating event messages across all members in a network, providing the fault-tolerance layer that underpins other HashiCorp tools such as Consul.

## Key features

- Decentralized membership with automatic node failure detection
- Gossip-based event broadcast across the whole cluster
- Custom event handlers and user-defined events
- Scales across large, or even malicious, networks with tunable consistency

## Notes for administrators

Because Serf is a foundational library, it is often embedded within orchestration tools rather than run directly; review whether an embedded use case is a better fit before deploying it standalone.

## Resources

- [Official documentation](https://www.serf.io)
- [Repository](https://github.com/hashicorp/serf)