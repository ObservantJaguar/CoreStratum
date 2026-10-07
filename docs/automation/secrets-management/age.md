---
title: Age
parent: Secrets Management
---

# Age

Age is a simple, modern, and secure file encryption tool designed as a lightweight alternative to PGP for encrypting files and secrets. It uses a small, auditable command surface and cryptographic algorithms based on ChaCha20-Poly1305, X25519, and HKDF, and it is the default encryption engine used by SOPS for file-level secret encryption.

## Key features

- Modern primitives including X25519, ChaCha20-Poly1305, and HKDF
- Small command-line surface with straightforward usage
- Native `age` and password-based encryption modes
- Built-in support in SOPS and many third-party tooling integrations

## Notes for administrators

Store recipient public keys in version control, but keep identity (private key) files out of Git and back them up securely.

## Resources

- [Official documentation](https://age-encryption.org)
- [Repository](https://github.com/FiloSottile/age)