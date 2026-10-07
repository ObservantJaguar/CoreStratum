---
title: Linux Namespaces
parent: Isolation Mechanisms
---

# Linux Namespaces

Namespaces are a Linux kernel feature that isolate and virtualise system resources so that processes inside a namespace see a private view of that resource. They are the backbone of container isolation, since each container gets its own process, network, mount, user, and other namespaces.

By giving each running environment separate namespaces, the kernel makes containers look and behave like isolated systems even though they share the host kernel.

## Notes for administrators

- Key namespace types include PID, Network, Mount, UTS, User, IPC and Cgroup namespaces.
- Combined with cgroups (resource limits) to form the isolation model used by containers.
- Managed directly with tools such as `unshare`, `nsenter` and `ip netns`.

## Resources

- [namespaces(7) manual page](https://man7.org/linux/man-pages/man7/namespaces.7.html)
- [Linux kernel source](https://github.com/torvalds/linux)