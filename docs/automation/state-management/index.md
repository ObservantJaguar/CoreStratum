---
title: State Management
parent: Infrastructure Automation
grand_parent: Tools
---

# State Management

State management covers tools and concepts for tracking, storing, and coordinating the state of infrastructure and automation processes. This category is reserved for platforms that record resource state, handle locking and sharing of state across teams, and reconcile declared configuration against actual resources.

A core example is Terraform State: Terraform records the state of managed resources in a state file, which it uses to plan and apply changes against the real world. Because the state file is the source of truth for what has been deployed, it must be protected against concurrent modification. Terraform uses state locking to ensure that only one process modifies state at a time, and remote backends (such as S3, Azure Storage, or Terraform Cloud) that store the state file outside the local machine so it can be shared and locked across a team. Related platforms here provide the distributed key-value stores and coordination services frequently used as backends, sources of truth, or discovery layers for such state.

## Programs

- [Consul](consul.md) - service discovery, health checking, and distributed KV store
- [Serf](serf.md) - decentralized cluster membership and failure detection
- [Etcd](etcd.md) - strongly consistent distributed key-value store for cluster state
- [Apache Zookeeper](zookeeper.md) - distributed coordination, naming, and synchronization