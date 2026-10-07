---
title: Flux CD
parent: GitOps and Delivery
---

# Flux CD

Flux CD (Flux) is a set of open-source technologies for automated continuous delivery on Kubernetes using the GitOps model. It keeps the cluster state synchronised with a Git repository, applying source-controlled manifests and managing Helm releases declaratively.

Flux is a CNCF graduated project that provides source, Kustomize and Helm controllers, giving a flexible toolkit for delivering applications and infrastructure driven entirely by git.

## Notes for administrators

- Synchronises cluster state from Git and remediates drift automatically.
- Supports both plain YAML manifests and Helm releases via dedicated controllers.
- Integrates with image automation and dependency update workflows.

## Resources

- [Flux CD documentation](https://fluxcd.io)
- [Flux2 on GitHub](https://github.com/fluxcd/flux2)
- [Flux getting started](https://fluxcd.io/get-started/)