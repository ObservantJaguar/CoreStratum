---
title: Linux Filesystems
parent: Filesystems
grand_parent: Tools
---

# Linux Filesystems

Linux filesystems handle the organization and storage of data on disks and other media. This category covers native Linux filesystems including journaling, snapshots, and layout considerations, along with special-purpose filesystems such as squashfs for compressed read-only images and tmpfs for RAM-backed storage.

- [ext4](ext4.md) — the default journaling filesystem for most Linux distributions.
- [XFS](xfs.md) — high-performance journaling filesystem for large files and parallel I/O.
- [Btrfs](btrfs.md) — copy-on-write filesystem with snapshots, checksums, and RAID.
- [ZFS (Linux)](zfs.md) — advanced copy-on-write filesystem and volume manager with RAID-Z.
- [F2FS](f2fs.md) — flash-friendly filesystem for NAND and solid-state storage.
- [OverlayFS](overlayfs.md) — union-mount filesystem underlying container image layers.