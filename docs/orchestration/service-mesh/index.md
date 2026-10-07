---
title: Service Mesh
parent: Cluster Orchestration
grand_parent: Tools
---

# Service Mesh

A service mesh is a dedicated infrastructure layer that handles communication between services in a microservices architecture. It provides traffic management, observability and security features — such as load balancing, retries, mTLS and distributed tracing — without changing the application code.

This is usually implemented by injecting lightweight proxy sidecars alongside every service, controlled by a central control plane. The sidecars form a data plane that governs all service-to-service traffic. Most of the data planes below rely on [Envoy](../../networking/load-balancing/envoy.md) as the underlying proxy.

- [Istio](istio.md) — comprehensive service mesh with Envoy sidecars and istiod control plane.
- [Linkerd](linkerd.md) — lightweight, low-resource service mesh for Kubernetes.
- [Consul Connect](consul-connect.md) — service mesh built on Consul's service discovery.
- [Cilium](cilium.md) — eBPF-based networking and sidecarless service mesh.
- [Kuma](kuma.md) — multi-platform service mesh on Envoy for Kubernetes and VMs.