---
title: SOPS
parent: Secrets Management
---

# SOPS

SOPS (Secrets OPerationS) is a command-line tool for encrypting the values of configuration and YAML, JSON, ENV, INI, and binary files while keeping their keys and structure readable. Files remain version-control friendly, so secrets can be stored securely in Git repositories and decrypted at deploy time, making it a foundational tool for GitOps-style secret handling.

## Key features

- Format-aware encryption that preserves file structure and readable keys
- Support for age, PGP, AWS KMS, GCP KMS, Azure Key Vault, and HashiCorp Vault as encryption backends
- Easy integration with Git workflows and CI/CD pipelines
- Binary file support via binary keys
- Local key caching and command-line oriented operation

## Resources

- [Official documentation](https://getsops.io)
- [Repository](https://github.com/getsops/sops)