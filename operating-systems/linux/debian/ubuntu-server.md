# Ubuntu Server

Ubuntu Server is a Debian‑based, production‑grade Linux distribution widely used in cloud environments, container platforms, CI/CD systems, virtualization nodes, and general infrastructure.  
It provides predictable release cycles, strong hardware support, extensive documentation, and deep integration with cloud‑native tooling.

This page describes Ubuntu Server’s architecture, release model, package ecosystem, and operational characteristics relevant to infrastructure and DevOps.

---

## Description

Ubuntu Server focuses on:

- cloud‑native workloads  
- containerized environments  
- virtualization and orchestration  
- predictable LTS releases  
- strong hardware compatibility  
- wide ecosystem adoption  
- extensive upstream and vendor support  

It is one of the most widely deployed Linux server distributions in modern infrastructure.

---

## Release Model

Ubuntu maintains two primary release types:

- **LTS (Long Term Support)**  
  - 5 years of standard support  
  - 10 years with ESM (Extended Security Maintenance)  
  - recommended for production  

- **Interim Releases**  
  - supported for 9 months  
  - used for testing new features  

LTS releases form the backbone of most enterprise deployments.

---

## Package Ecosystem

Ubuntu uses the APT ecosystem inherited from Debian:

- `.deb` package format  
- `dpkg` low‑level tool  
- `apt`, `apt-get`, `apt-cache` high‑level tools  
- PPAs (Personal Package Archives) for additional software  
- Snap packages (optional, not required for server use)  

Ubuntu maintains its own repositories, synchronized and adapted from Debian.

---

## Architecture Notes

Key architectural characteristics:

- monolithic Linux kernel  
- systemd init system  
- glibc userland  
- AppArmor mandatory access control (default)  
- predictable filesystem hierarchy (FHS compliant)  
- cloud‑init integration for provisioning  
- strong virtualization and container support  

---

## Server Use Cases

Ubuntu Server is widely used for:

- cloud VMs (AWS, Azure, GCP, OpenStack)  
- Kubernetes nodes  
- Docker/Podman container hosts  
- CI/CD runners  
- virtualization nodes (KVM/QEMU)  
- microservices and distributed systems  
- general infrastructure services  

Its ecosystem and tooling make it ideal for cloud‑native environments.

---

## Cloud & Infrastructure Features

- **cloud‑init** — automated provisioning  
- **netplan** — declarative network configuration  
- **Landscape** — enterprise management  
- **MAAS** — bare‑metal provisioning  
- **LXD** — system containers and virtual machines  
- **Canonical Livepatch** — kernel patching without reboot  

---

## Related Distributions

- **[Debian](debian.md)**  
- **[Devuan](devuan.md)**  
- **[LMDE](lmde.md)**  
- **[MX Linux](mx-linux.md)**  
- **[Kali Linux](kali.md)**  
- **[Raspberry Pi OS](raspberry-pi-os.md)**  
- **[Parrot OS](parrot.md)**  
- **[PureOS](pureos.md)**  

---

## Related Concepts

- **[APT Ecosystem](concepts/apt.md)**  
- **[Release Model](concepts/release-model.md)**  
- **[Init Systems](../../concepts/init-systems.md)**  
- **[Filesystems](../../concepts/filesystems.md)**  
- **[Bootloaders](../../concepts/bootloaders.md)**  

---

## Purpose

This page provides a structured reference for:

- Ubuntu Server administration  
- cloud and container‑native deployments  
- infrastructure and platform engineering  
- virtualization and orchestration environments  

Ubuntu Server is the most widely used Debian‑based system in modern infrastructure.
