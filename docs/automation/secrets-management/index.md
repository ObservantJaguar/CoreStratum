---
title: Secrets Management
parent: Infrastructure Automation
grand_parent: Tools
---

# Secrets Management

Secrets management covers tools for securely storing, rotating, and distributing sensitive values such as passwords, API keys, and certificates. The platforms in this category provide centralized secret storage, access control, and auditability for automated environments, ranging from full secret-management servers to file-level encryption and Kubernetes-native operators.

## Programs

- [HashiCorp Vault](vault.md) - centralized secret storage, dynamic secrets, and encryption
- [OpenBao](openbao.md) - community-governed fork of HashiCorp Vault
- [SOPS](sops.md) - format-aware encryption of secrets stored in Git
- [Sealed Secrets](sealed-secrets.md) - Kubernetes-native encrypted secrets for GitOps
- [External Secrets Operator](external-secrets.md) - syncs secrets from external providers into Kubernetes
- [Age](age.md) - simple, modern file encryption for secrets