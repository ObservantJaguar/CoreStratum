---
title: Cluster Operators
parent: Cluster Orchestration
grand_parent: Tools
---

# Cluster Operators

Operators are a pattern for automating the lifecycle of a specific application or component inside a cluster. An operator encodes operational knowledge in software, so it can install, configure, monitor and repair an application automatically as its state changes.

Rooted in the Kubernetes operator pattern, this category covers both the operator framework itself and the operators that manage databases, messaging and other stateful workloads on top of a cluster.

- [Operator Lifecycle Manager](olm.md) — manages the install and upgrade lifecycle of operators.
- [Kubebuilder](kubebuilder.md) — Go framework for building Kubernetes operators and controllers.
- [Operator SDK](operator-sdk.md) — tooling for building operators in Go, Ansible, and Helm.

[Helm](../package-management/helm.md), documented under Cluster Package Management, is frequently used to deploy and manage operators themselves.