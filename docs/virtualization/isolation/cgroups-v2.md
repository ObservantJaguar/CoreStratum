---
title: Cgroups v2
parent: Isolation Mechanisms
---

# Cgroups v2

Cgroups (control groups) v2 is the modern Linux kernel mechanism for limiting, accounting for and isolating the resource usage of process groups. It provides hierarchical limits on CPU, memory and I/O, which is essential for fair resource sharing on multi-tenant hosts and for containers.

The unified cgroups v2 hierarchy replaces the older v1 model, offering a single consistent tree and letting administrators cap and monitor resource consumption reliably.

## Notes for administrators

- Provides controllers for cpu, memory, io, cpuset, pids, hugetlb and more.
- Works together with Linux namespaces to provide the isolation model used by containers.
- Exposed through the `/sys/fs/cgroup` unified hierarchy and tools such as `systemd`.

## Resources

- [cgroup-v2 documentation on kernel.org](https://docs.kernel.org/admin-guide/cgroup-v2.html)
- [Linux kernel source](https://github.com/torvalds/linux)