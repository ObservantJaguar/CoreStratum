---
title: RAID
parent: Storage
grand_parent: Tools
---

# RAID

RAID (Redundant Array of Independent Disks) combines multiple physical disks into logical volumes for improved performance and fault tolerance, using schemes such as mirroring (RAID 1), striping with parity (RAID 5), and dual parity (RAID 6). This category documents software RAID tools and filesystems that implement their own redundancy levels.

- [mdadm](mdadm.md) — the standard Linux tool for managing software RAID arrays.
- [OpenZFS](openzfs.md) — ZFS with RAID-Z parity redundancy, snapshots, and checksums.
- **Btrfs RAID** — the Btrfs filesystem implements its own RAID levels for metadata and data (part of the Linux kernel, not a separate tool).