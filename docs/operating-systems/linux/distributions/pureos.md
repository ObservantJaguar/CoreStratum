---
title: PureOS
parent: Linux Distributions
---

# PureOS

PureOS is a Debian-based Linux distribution developed by Purism and endorsed by the Free Software Foundation (FSF).  
It is built entirely from free software, using Debian as its upstream base, and focuses on privacy, security, and freedom-respecting computing environments.

This page describes PureOS's architecture, release model, package ecosystem, and operational characteristics relevant to infrastructure, DevOps, and security engineering.

---

## Description

PureOS focuses on:

- 100% free software (FSF-endorsed)  
- privacy-focused defaults  
- secure communication stacks  
- minimal upstream patching  
- Debian-based stability  
- reproducible and auditable systems  

PureOS is used in environments where software freedom, transparency, and privacy are critical.

---

## Release Model

PureOS maintains two branches:

- **Stable** — based on Debian Stable, conservative and long-term  
- **Rolling** — based on Debian Testing, more up-to-date  

Both branches contain only free software packages, following strict FSF guidelines.

---

## Package Ecosystem

PureOS uses the Debian APT ecosystem:

- `.deb` package format  
- `dpkg` low-level tool  
- `apt`, `apt-get`, `apt-cache` high-level tools  
- Debian repositories (filtered for free software)  
- PureOS repositories for privacy-focused components  

PureOS excludes:

- proprietary firmware  
- proprietary drivers  
- non-free repositories  
- non-free codecs  
- proprietary browser components  

This ensures full auditability and compliance with FSF standards.

---

## Architecture Notes

Key architectural characteristics:

- monolithic Linux kernel (deblobbed)  
- systemd init system  
- glibc userland  
- Debian-compliant filesystem hierarchy  
- strict free-software policy  
- hardened privacy defaults  

PureOS includes:

- deblobbed kernel  
- privacy-focused browser (PureBrowser)  
- secure communication stack  
- sandboxed application environments  

---

## Privacy & Security Features

PureOS provides:

- hardened browser configuration  
- secure defaults for networking  
- privacy-focused applications  
- strict free-software compliance  
- reproducible builds  
- minimal telemetry (none by default)  

It is widely used in privacy-focused environments and secure workstations.

---

## Server Use Cases

PureOS can be used for:

- privacy-focused servers  
- secure communication nodes  
- research environments  
- reproducible infrastructure  
- free-software-only deployments  

PureOS is **not** intended for:

- general-purpose production servers  
- cloud-native workloads  
- container hosts  
- virtualization nodes  

For those roles, Debian or Ubuntu Server are preferred.

---

More about the family: [Debian Family](index.md)