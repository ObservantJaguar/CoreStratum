---
title: OpenBao
parent: Secrets Management
---

# OpenBao

OpenBao is an open-source, community-driven fork of HashiCorp Vault that preserves the core functionality of centralized secret management while operating under an open governance model. It provides encrypted storage, access control, audit logging, and a broadly compatible API, offering a maintained alternative for teams that prefer a fully open governance and licensing approach.

## Key features

- API-compatible with HashiCorp Vault for a smooth migration path
- Encrypted secret storage with dynamic secret generation and leases
- Multiple authentication methods and fine-grained access policies
- Audit logging and audit device support
- Community-governed development and maintenance

## Notes for administrators

Because OpenBao is a Vault fork, existing Vault workflows, documented tooling, and migration tooling often apply with minimal changes. Always review the current release notes for compatibility details before moving production workloads.

## Resources

- [Official documentation](https://openbao.org)
- [Repository](https://github.com/openbao/openbao)