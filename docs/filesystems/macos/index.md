---
title: macOS Filesystems
parent: Filesystems
grand_parent: Tools
---

# macOS Filesystems

macOS filesystems handle data storage on Apple computers. This category describes the native filesystems used on macOS and the storage features built around them.

## Filesystems

- **APFS** (Apple File System) — the default filesystem of modern macOS. It is a copy-on-write filesystem with native support for snapshots, cloning, space sharing across volumes, and full-disk encryption.
- **HFS+** — the legacy macOS filesystem used before APFS, supporting journaling, case-insensitive names, and hard links. It remains relevant for older volumes and interoperability.

macOS storage features such as Time Machine backups and containerized APFS volumes build on the APFS snapshot and volume-management capabilities.