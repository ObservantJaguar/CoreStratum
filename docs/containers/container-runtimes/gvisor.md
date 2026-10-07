---
title: gVisor
parent: Container Runtimes
---

# gVisor

gVisor is a user-space kernel for containers developed by Google. It intercepts system calls made by containerized applications and handles them in an isolated user-space environment, adding an extra security boundary between the workload and the host kernel.

Its enhanced isolation makes it suitable for running untrusted or multi-tenant workloads, at the cost of some compatibility and performance.

## Resources

- [Official website](https://gvisor.dev)
- [Repository](https://github.com/google/gvisor)