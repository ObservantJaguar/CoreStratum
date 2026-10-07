---
title: Cluster Package Management
parent: Cluster Orchestration
grand_parent: Tools
---

# Cluster Package Management

Cluster package management covers the tools that install, upgrade, configure and uninstall applications in a cluster, in the same way a package manager does for a single operating system. These tools bundle applications together with their dependencies and reconcile them against the cluster state.

This category documents packaging and templating solutions that sit above the scheduler. The Cloud Native Application Bundle (CNAB) specification extends this idea to bundle and run distributed applications across runtimes, complementing Helm charts and Kubernetes-native tools.

- [Helm](helm.md) — the standard package manager and charting tool for Kubernetes.
- [Kustomize](kustomize.md) — declarative base-and-overlay Kubernetes configuration management.