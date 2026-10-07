---
title: KVM
parent: Hypervisors
---

# KVM

KVM (Kernel-based Virtual Machine) is a virtualisation module in the Linux kernel that turns a Linux host into a type-1 hypervisor using the hardware virtualisation extensions of modern CPUs. Each virtual machine runs as a regular Linux process with normal scheduling and tooling.

KVM is the foundation of most production Linux virtualisation, and when combined with QEMU or libvirt it provides a complete platform for running and managing virtual machines on commodity hardware.

## Notes for administrators

- Built directly into the Linux kernel, so no separate kernel is needed.
- Integrates with cgroups and Linux process management for resource control.
- Often orchestrated through libvirt, QEMU command-line tools or management layers such as Proxmox.

## Resources

- [KVM — linux-kvm.org](https://www.linux-kvm.org)
- [KVM documentation on kernel.org](https://www.linux-kvm.org/page/Documents)
- [KVM code in the Linux kernel](https://git.kernel.org)