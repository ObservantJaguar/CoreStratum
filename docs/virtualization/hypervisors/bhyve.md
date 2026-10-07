---
title: bhyve
parent: Hypervisors
---

# bhyve

bhyve is the modern hypervisor built into FreeBSD. It uses the hardware virtualisation extensions of the CPU to run guest operating systems with low overhead, integrated directly into the FreeBSD kernel.

For administrators running FreeBSD, bhyve provides a native virtualisation solution without additional software, and it is the platform behind the FreeBSD VM infrastructure as well as commercial products such as VMware's Bundle and pfSense's virtualisation.

## Notes for administrators

- Kernel-resident and controlled via the bhyve utilities, libvirt or management front ends.
- Supports virtual machines with virtio devices for good performance.
- Typically used together with ZFS for snapshots and space-efficient storage.

## Resources

- [bhyve — FreeBSD Wiki](https://wiki.freebsd.org/bhyve)
- [FreeBSD Handbook: Virtualization](https://docs.freebsd.org/en/books/handbook/virtualization/)
- [FreeBSD source on GitHub](https://github.com/freebsd/freebsd-src)