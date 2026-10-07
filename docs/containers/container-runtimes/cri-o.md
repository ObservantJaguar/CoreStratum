---
title: CRI-O
parent: Container Runtimes
---

# CRI-O

CRI-O is a lightweight container runtime designed specifically for Kubernetes. It implements the Kubernetes Container Runtime Interface (CRI) and uses runc (or other OCI runtimes) to execute containers, eliminating the need for a separate engine layer.

Its minimal design and focus on standards make it a common choice for Kubernetes clusters that want to avoid Docker's overhead while staying OCI-compliant.

## Resources

- [Official website](https://cri-o.io)
- [Repository](https://github.com/cri-o/cri-o)