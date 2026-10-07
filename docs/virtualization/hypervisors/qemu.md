---
title: QEMU
parent: Hypervisors
---

# QEMU

QEMU is a generic, open-source machine emulator and virtualiser. It can run unmodified guest operating systems by emulating a full computer, and with KVM acceleration on Linux it provides near-native performance as a hypervisor.

QEMU is the most common user-space front end for KVM virtual machines and also drives emulation in development and testing environments where real hardware is not available.

## Notes for administrators

- Can act as a pure software emulator or as an accelerator alongside KVM/HVF/Xen.
- Supports a very wide range of guest architectures and hardware.
- Frequently combined with libvirt and management platforms such as Proxmox and OpenStack.

## Resources

- [QEMU — qemu.org](https://www.qemu.org)
- [QEMU documentation](https://www.qemu.org/docs/)
- [QEMU on GitLab](https://gitlab.com/qemu-project/qemu)