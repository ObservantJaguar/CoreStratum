---
title: Open Standards
parent: Foundations
grand_parent: Theory
---

# Open Standards

Open standards are publicly available specifications developed through transparent, consensus-based processes that guarantee fair implementation, interoperability and long-term stability. They are maintained by recognised standards bodies and are typically available for free or under open terms, which prevents vendor lock-in and enables competing implementations.

Open standards matter for infrastructure because they ensure that products from different vendors can interoperate today and remain compatible for decades. This category covers the standards that underpin open systems, from file formats to communication and security specifications.

## Operating-system interfaces

- **POSIX** — the Portable Operating System Interface standard (IEEE 1003, ISO/IEC 9945) defines the API, command-line and utilities of a Unix-like system. It is why code and skills port between Linux, BSD and macOS.
- **Linux Standard Base (LSB)** — a standardisation project that defines the core ABI and package layout for Linux distributions.
- **Filesystem Hierarchy Standard (FHS)** — defines the directory layout of Unix-like systems (`/etc`, `/var`, `/usr`, `/srv`...).

## Networking and security

- **IETF RFCs** — the Requests for Comments are the working documents of the Internet Engineering Task Force; they define the open protocols of the Internet (TCP/IP, HTTP, DNS, TLS, SMTP...).
- **DNSSEC** — standardised extensions to DNS that authenticate responses with digital signatures.
- **OAuth 2.0 and OpenID Connect** — industry-standard protocols for delegated authorisation and authentication, used by [Keycloak](../../security/authentication/keycloak.md) and [Authentik](../../security/authentication/authentik.md).
- **SAML** — Security Assertion Markup Language, a standard for exchanging authentication and authorisation data between parties, widely used in enterprise SSO.
- **FIDO2 / WebAuthn** — open standard for passwordless and second-factor authentication using public-key cryptography.

## Data and file formats

- **Unicode and UTF-8** — the universal character set and its dominant encoding, used by virtually all modern software for text.
- **JPEG, PNG, WebP** — open raster image formats; PNG and WebP are royalty-free, unlike the older GIF (patent-encumbered in the 1990s).
- **ODF (OpenDocument)** — an open, ISO-standardised document format (ISO/IEC 26300) used by LibreOffice, OpenDocument Editors and [OnlyOffice](../../communications/hubs/onlyoffice.md) interoperability.
- **PDF** — the Portable Document Format, published as an ISO standard (ISO 32000) since 2008, making it an open standard controlled by ISO rather than a single vendor.
- **SQL** — the standardised query language for relational databases (ISO/IEC 9075).

## Containers and clouds

- **OCI (Open Container Initiative)** — standards for container images (image-spec) and container runtimes (runtime-spec); implemented by [Docker](../../containers/container-engines/docker.md), [containerd](../../containers/container-engines/containerd.md) and [runc](../../containers/container-runtimes/runc.md).
- **CNI** — the Container Network Interface standard for configuring network interfaces in Linux containers.
- **CSI** — the Container Storage Interface standard for exposing storage systems to container orchestration platforms.
- **CRI** — the Container Runtime Interface used by Kubernetes to talk to runtimes like [CRI-O](../../containers/container-runtimes/cri-o.md) and containerd.
- **CNAB** — Cloud-Native Application Bundle, a standard for packaging and running distributed applications.

## Related pages

- [Open Protocols](../protocols/index.md) — the wire protocols built on these standards.
- [Licensing](../licenses/index.md) — the legal framework that keeps these standards' implementations open.
- [Foundations](../index.md)