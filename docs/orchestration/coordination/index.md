---
title: Distributed Coordination
parent: Cluster Orchestration
grand_parent: Tools
---

# Distributed Coordination

Distributed coordination services provide the consensus, locking, leader election and shared configuration that distributed systems need to agree on state in a reliable way. They are the foundation on top of which many schedulers and clustering products are built.

A coordination service typically stores small, frequently read key-value data with strong consistency guarantees and notifications, letting distributed components coordinate without a single point of failure.

- [etcd](../../automation/state-management/etcd.md) — consistent key-value store and Kubernetes backing store.
- [Zookeeper](../../automation/state-management/zookeeper.md) — hierarchical coordination and group services.
- [Consul](../../automation/state-management/consul.md) — service discovery, health checking and key-value store.

Redis Cluster (documented under Databases) also offers a limited coordination layer via its clustering and Lua-scripting capabilities, while ClickHouse Keeper provides a ZooKeeper-compatible coordination service specifically for ClickHouse replication.