---
title: Take a Quick Snapshot with btrfs/ZFS
parent: Recipes
grand_parent: Guides
---

# Take a Quick Snapshot with btrfs/ZFS

## Goal

Make an instant point-in-time snapshot of a filesystem before a risky operation, and roll it back if needed.

## Task

Before an upgrade or dangerous command, snapshot the data so it can be restored instantly.

## Steps

### btrfs

1. Snapshot a subvolume read-only (immutable rollback point):

```bash
sudo btrfs subvolume snapshot -r /mnt/data /mnt/data/.snapshot-$(date +%F-%T)
```

2. On btrfs the subvolume must be a real subvolume, not an arbitrary directory.

### ZFS

1. Snapshot a dataset (atomic, near-zero cost):

```bash
sudo zfs snapshot tank/data@before-op
```

### Rollback

- ZFS rollback to the snapshot (discards newer snapshots of that dataset):

```bash
sudo zfs rollback tank/data@before-op
```

- btrfs - restore a read-only snapshot by cloning it over the target:

```bash
sudo rm -rf /mnt/data && sudo btrfs subvolume snapshot -r /mnt/data/.snapshot-2026-10-08 /mnt/data
```

(or use `btrfs subvolume snapshot` of a rw snapshot to preserve current state).

## Verification

- The snapshot exists:

```bash
sudo btrfs subvolume list /mnt/data
```

- Or for ZFS:

```bash
zfs list -t snapshot
```

## Gotchas

- **A snapshot is not an external backup** - a snapshot lives on the same drive/array as the data; a disk failure or `rm` of the pool destroys both the data and the snapshot. Always keep a real off-box backup for anything you cannot re-create.
- **ZFS rollback discards state** - it reverts the dataset to the snapshot and can only roll back to the most recent snapshot unless you `--force` (which destroys the snapshots in between) or clone first. `zfs rollback -r` forces the discard.
- **btrfs snapshots need subvolumes** - `btrfs subvolume snapshot` errors on a plain directory; the target must be a subvolume (check `btrfs subvolume list /`).
- **Read-only snapshots can't be mounted directly to write** - mount rw only after making it writable (`btrfs property set ... ro false` or a new writable snapshot).

## Related

- [Filesystem concepts](../../storage/backup/zfs-snapshots.md)
- [Backup strategy](../../storage/backup/index.md)
- [rsync transfer](rsync-transfer.md)