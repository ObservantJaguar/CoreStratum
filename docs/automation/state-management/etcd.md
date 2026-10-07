---
title: Etcd
parent: State Management
---

# Etcd

Etcd is a strongly consistent, distributed key-value store that provides reliable storage for the state and configuration of distributed systems. It uses the Raft consensus algorithm to guarantee consistency across replicated nodes and is widely known as the foundational store behind Kubernetes clusters for persisting cluster state.

## Key features

- Strongly consistent data storage using the Raft consensus protocol
- Simple gRPC and HTTP/JSON client APIs
- Watch support for real-time change notifications across the cluster
- Lease-based key expiration and cluster membership management
- TLS and role-based access control for secure access

## Notes for administrators

Health and performance of etcd directly affect the stability of dependent systems such as Kubernetes; tune disk I/O, snapshotting, and quorum-aware sizing carefully, and always back up the data dir.

## Resources

- [Official documentation](https://etcd.io)
- [Repository](https://github.com/etcd-io/etcd)