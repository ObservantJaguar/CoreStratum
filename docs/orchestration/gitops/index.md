---
title: GitOps and Delivery
parent: Cluster Orchestration
grand_parent: Tools
---

# GitOps and Delivery

GitOps is a model for continuous delivery in which a Git repository is the single source of truth for the desired state of a system. Operators and delivery tools continuously compare the live cluster state with the state described in Git and reconcile any drift automatically.

This approach makes deployments auditable, reviewable and rollback-friendly because every change is a commit that can be inspected and reverted.

## Tools

- [Argo CD](argo-cd.md)
- [Flux CD](flux-cd.md)