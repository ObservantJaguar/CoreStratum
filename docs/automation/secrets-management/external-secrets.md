---
title: External Secrets Operator
parent: Secrets Management
---

# External Secrets Operator

External Secrets Operator is a Kubernetes operator that synchronizes secrets from external systems, such as HashiCorp Vault, AWS Secrets Manager, GCP Secret Manager, and Azure Key Vault, into the cluster as native Kubernetes Secrets. Supported by many external providers through a provider API, it centralizes secret access from GitOps-managed clusters while delegating authority to the underlying secret backends.

## Key features

- Syncs secrets from dozens of external providers and secret stores
- Native Kubernetes Secret objects as the output
- Secret pull-based or push-based synchronization models
- Centralized secret access management for GitOps workflows

## Notes for administrators

Access and permission for the external provider is configured per ExternalSecret cluster resource; ensure the operator's provider credentials are scoped to the minimum required permissions.

## Resources

- [Official documentation](https://external-secrets.io)
- [Repository](https://github.com/external-secrets/external-secrets)