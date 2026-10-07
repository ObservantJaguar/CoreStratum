---
title: Containerd
parent: Container Engines
---

# Containerd

Containerd is an industry-standard core container runtime. It manages the complete lifecycle of container images and containers on a host, including image transfer and storage, container execution, supervision and low-level storage and network interfaces.

Designed to be embedded, containerd serves as the container runtime within Docker, Kubernetes and many cloud-native platforms, providing a stable and minimal foundation for higher-level tooling.

## Notes for administrators

- Runs as a daemon with a clearly defined, small API surface.
- Implements the Open Container Initiative (OCI) image and runtime specifications.
- Used natively by Kubernetes through the CRI plugin and by Docker Engine underneath.

## Resources

- [Containerd documentation](https://containerd.io)
- [Containerd on GitHub](https://github.com/containerd/containerd)
- [Containerd CRI plugin](https://github.com/containerd/containerd/tree/main/contrib/cri)