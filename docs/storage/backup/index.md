---
title: Backup and Disaster Recovery
parent: Storage
grand_parent: Tools
---

# Backup and Disaster Recovery

Backup and disaster recovery covers tools for ensuring data resilience and creating restore points. The category is organized into four groups: snapshot mechanisms for filesystem state capture, deduplication-focused backup tools, specialized enterprise backup systems, and transport utilities for copying data to off-site storage.

## Snapshots

- [ZFS Snapshots](zfs-snapshots.md) — instantaneous atomic filesystem snapshots.
- [Btrfs Snapshots](btrfs-snapshots.md) — Linux filesystem snapshots with incremental transfer.
- [Timeshift](timeshift.md) — system state snapshots for Linux rollback.
- [Snapper](snapper.md) — specialized utility for managing filesystem snapshots.

## Deduplication

- [BorgBackup](borgbackup.md) — backup with efficient deduplication, compression, and encryption.
- [Restic](restic.md) — fast backup tool with native S3 support.
- [Duplicacy](duplicacy.md) — cross-platform tool with unique deduplication.

## Enterprise

- [Barman](barman.md) — backup and recovery solution for PostgreSQL.
- [Velero](velero.md) — backup and migration tool for Kubernetes resources.
- [Bacula](bacula.md) — scalable enterprise-level network backup system.
- [Proxmox Backup Server](proxmox-backup-server.md) — backup of Proxmox VMs and containers.
- [UrBackup](urbackup.md) — client/server backup with an easy web interface.
- [Duplicati](duplicati.md) — encrypted backup to cloud, FTP and NAS destinations.

## Transport

- [Rclone](rclone.md) — synchronization of files with dozens of cloud storages.