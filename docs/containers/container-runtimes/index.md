---
title: Container Runtimes
parent: Containers and Runtimes
grand_parent: Tools
---

# Container Runtimes

A **container runtime** is the low-level component responsible for actually running a container: it sets up the namespaces and cgroups, applies the configuration defined in the image, and manages the lifecycle of the container processes on the host.

It is useful to distinguish the runtime from the **container engine** described in the Container Engines category: the engine provides the user-facing tools that build, pull and orchestrate containers, while the runtime is the layer underneath that executes them. An engine typically delegates the actual execution to a runtime.

This category documents the runtimes that implement the Open Container Initiative specifications and provide the execution layer for engines and platforms such as Kubernetes.

- [runc](runc.md) — reference OCI runtime, default under Docker and containerd.
- [CRI-O](cri-o.md) — Kubernetes CRI runtime using OCI runtimes underneath.
- [gVisor](gvisor.md) — user-space kernel adding isolation between workloads and the host.
- [Kata Containers](kata-containers.md) — containers running inside lightweight VMs.