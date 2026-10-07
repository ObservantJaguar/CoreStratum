---
title: Argo CD
parent: GitOps and Delivery
---

# Argo CD

Argo CD is a declarative, GitOps-native continuous delivery tool for Kubernetes. It stores the desired application state in a Git repository, syncs that state to the cluster, and continuously verifies that the running applications match what is described in Git.

Argo CD automates the deployment of Kubernetes manifests, Helm charts, Kustomize configurations and more, handling rollbacks, health assessment and multi-cluster deployment from a central location.

## Notes for administrators

- Application state is defined and audited in Git; anything in Git is reproducible.
- Supports sync policies, automatic health assessment and rollback to prior states.
- Provides a web UI, CLI and API for managing applications across clusters.

## Resources

- [Argo CD documentation](https://argo-cd.readthedocs.io)
- [Argo CD on GitHub](https://github.com/argoproj/argo-cd)
- [Argo CD getting started](https://argo-cd.readthedocs.io/en/stable/getting_started/)