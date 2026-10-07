---
title: Provisioning
parent: Infrastructure Automation
grand_parent: Tools
---

# Provisioning

Provisioning covers tools and practices for creating and initializing infrastructure resources before configuration management takes over. The platforms in this category handle the automated bring-up of bare-metal, virtual, and cloud resources, from image building and virtual environments to bare-metal installation servers.

Related provisioning concerns are also covered in the [Infrastructure as Code](../iac/index.md) category, including [Cloud-Init](../iac/cloud-init.md), the industry-standard tool for bootstrapping cloud instances during first boot.

## Programs

- [HashiCorp Vagrant](vagrant.md) - reproducible virtual development environments
- [HashiCorp Packer](packer.md) - building identical machine images across platforms
- [Foreman](foreman.md) - bare-metal and virtual host lifecycle management
- [Cobbler](cobbler.md) - Linux installation server for network-based provisioning
- [MAAS](maas.md) - bare-metal provisioning from Canonical as a service