---
title: Windows Filesystems
parent: Filesystems
grand_parent: Tools
---

# Windows Filesystems

Windows filesystems manage data storage on Microsoft Windows operating systems. This category describes the native filesystems available on Windows and the scenarios each one fits.

## Filesystems

- **NTFS** — the default filesystem for Windows system and data volumes. It supports journaling, file and folder permissions (ACLs), encryption (EFS), compression, hard links, and shadow copies.
- **ReFS** (Resilient File System) — a modern filesystem designed for high availability and large storage pools, with built-in resilience and integrity checking. Used mainly in Storage Spaces and Windows Server scenarios.
- **exFAT** — a lightweight filesystem for removable media and flash drives, supporting very large files and cross-platform interchange without NTFS overhead.
- **FAT32** — the legacy filesystem with maximal compatibility across devices and operating systems, limited to files up to 4 GB.

Windows storage management builds on these filesystems through tools such as Disk Management, Storage Spaces, and volume shadow copies.