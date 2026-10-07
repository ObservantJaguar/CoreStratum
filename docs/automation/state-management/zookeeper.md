---
title: Apache Zookeeper
parent: State Management
---

# Apache Zookeeper

Apache ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. It coordinates distributed applications through a replicated, hierarchically organized namespace maintained with strong consistency, making it a long-standing solution for distributed coordination and state.

## Key features

- Hierarchical namespace with znode data and watch-based notifications
- Strong consistency for reads and writes via a leader-based protocol
- Distributed locks, leader election, and configuration management primitives
- Persistent and ephemeral znodes for registry and state use cases

## Notes for administrators

ZooKeeper requires an odd-sized ensemble to maintain quorum; monitor session counts and transaction throughput, and note that modern projects increasingly prefer etcd or Consul for greenfield deployments.

## Resources

- [Official documentation](https://zookeeper.apache.org)
- [Repository](https://github.com/apache/zookeeper)