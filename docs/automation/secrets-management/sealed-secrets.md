---
title: Sealed Secrets
parent: Secrets Management
---

# Sealed Secrets

Sealed Secrets is a Kubernetes-native tool from Bitnami that encrypts secrets into SealedSecret custom resources that are safe to store in Git. A controller running in the cluster decrypts the SealedSecrets back into regular Kubernetes Secret objects, allowing secrets to be managed declaratively and committed to a GitOps repository without exposing their plaintext values.

## Key features

- SealedSecret custom resource stored safely in Git repositories
- Cluster-side controller that decrypts into standard Kubernetes Secrets
- RSA encryption bound to a scoped set of namespaces, names, and labels
- Native integration with kubectl and GitOps workflows

## Notes for administrators

The controller's encryption key is stored in the cluster, so the sealed secret binding should be re-created if a cluster is rebuilt; back it up to recover access to existing data.

## Resources

- [Official documentation](https://bitnami-labs.github.io/sealed-secrets)
- [Repository](https://github.com/bitnami-labs/sealed-secrets)