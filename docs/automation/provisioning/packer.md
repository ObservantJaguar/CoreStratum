---
title: HashiCorp Packer
parent: Provisioning
---

# HashiCorp Packer

HashiCorp Packer is a tool for creating identical machine images across multiple platforms from a single source template. It automates the build of pre-baked images for cloud, virtualization, and container platforms, resulting in consistent base images that can be deployed directly, speeding up provisioning and improving reproducibility.

## Key features

- Single source template building identical images on many platforms
- Parallel builds across multiple source builders
- Support for major cloud providers, hypervisors, and container platforms
- Post-processors for image handling and artifact generation
- Integration with configuration management tools to pre-configure images

## Notes for administrators

Pre-baked images reduce first-boot provisioning time and surface fewer runtime failures; keep the image build pipeline in version control and rebuild on a schedule to stay current with security updates.

## Resources

- [Official documentation](https://www.packer.io)
- [Repository](https://github.com/hashicorp/packer)