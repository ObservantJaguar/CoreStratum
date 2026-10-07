---
grand_parent: Practice
title: Backup with restic and Borg
parent: Guides
---

# Backup with restic and Borg

## Goal

A working, testable backup strategy for servers and container data using **restic** or **BorgBackup**. Both tools provide deduplication, compression and encryption, so backups are small, safe to store offsite and cannot be read without the key. By the end of this guide you will have:

- daily automated backups of chosen directories and Docker volumes
- encrypted backups stored locally and (optionally) in offsite/object storage
- retention policy (keep a sensible number of snapshots)
- a documented restore procedure that has actually been tested

## Scope and out of scope

**In scope:**
- restic and Borg as the two main tools, with a comparison
- backup of directories and Docker volumes
- automation via systemd timers
- encryption and offsite storage (S3-compatible, or SFTP/SSH)
- retention and integrity checking
- restore verification

**Out of scope:**
- full disk imaging (see [ZFS Snapshots](../storage/backup/zfs-snapshots.md), [Timeshift](../storage/backup/timeshift.md))
- database-level backup tools (see [Barman](../storage/backup/barman.md), database pages)
- cluster disaster recovery (that needs its own design)

## Prerequisites

- SSH access to the server being backed up
- A destination: local disk, another server via SSH/SFTP, or an S3-compatible bucket
- Neither tool requires a daemon; both are single binaries

## Choosing the tool

| Attribute | restic | BorgBackup |
|---|---|---|
| Model | Repository of snapshots, no built-in repo server | Repository; official `borg serve` command for network backups |
| Deduplication | Content-defined chunking | Chunking by content, very effective |
| Encryption | AES-256, blind rotation possible | AES-CTR + HMAC (repokey/keyfile) |
| S3 / object storage | Native, first-class | Via `rclone remotes` (works well) |
| Parallelism | Good for large trees | Also good, slightly simpler behavior |
| Backup from arbitrary hosts | Very easy (single binary) | Easy |

For most SMB self-hosted setups both are excellent. restic has simpler S3 integration; Borg is often a bit more efficient on disk and has a smooth `borg mount` workflow.

## Architecture

```
                                       РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’
  РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’               РІвЂќвЂљ   Backup target        РІвЂќвЂљ
  РІвЂќвЂљ  Server            РІвЂќвЂљ  restic РІРЏВµ    РІвЂќвЂљ   (local disk, SSH,    РІвЂќвЂљ
  РІвЂќвЂљ  /etc, /srv,       РІвЂќвЂљРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’      РІвЂќвЂљ    S3-compatible,      РІвЂќвЂљ
  РІвЂќвЂљ  docker volumes    РІвЂќвЂљ       РІвЂќвЂљ      РІвЂќвЂљ    Borg repo via ssh)  РІвЂќвЂљ
  РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ       РІвЂќвЂљ      РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ¬РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ
          РІвЂќвЂљ                  cron/timer           РІвЂќвЂљ
          РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂ“С”  encrypted         РІвЂќвЂљ
                               snapshots          РІвЂќвЂљ
                                                  РІвЂ“С
                            Retention policy: daily/weekly/monthly
```

## Roadmap

### Stage 1 — Install and initialize

**restic:**

```bash
sudo apt install restic           # or download the binary from restic.net
restic init --repo sftp:backup@nas01.example.com:/backups/restic   # local repo:
# restic init --repo /mnt/backup/restic
```

You will be asked for a repository password. **Store it in a password manager and in a sealed envelope** — without it the backups are unrecoverable.

**BorgBackup:**

```bash
sudo apt install borgbackup
borg init --encryption=repokey-blake2 ssh://backup@nas01.example.com/backups/borg
# or locally: borg init --encryption=repokey-blake2 /mnt/backup/borg
```

### Stage 2 — Define what to back up

- [ ] List the directories that hold valuable state: `/etc`, `/root`, `/srv`, service data
- [ ] Docker volumes: either back up `/var/lib/docker/volumes` or use `docker run --rm -v` to tar/restic the volume contents
- [ ] Databases: dump them first (e.g. `pg_dump`), then back up the dump — never snapshot a live DB file without proper support
- [ ] Decide on exclusions: caches, temp files, large media that is already mirrored

### Stage 3 — First backup and check

**restic:**

```bash
restic -r /mnt/backup/restic backup /etc /srv /var/lib/docker/volumes
restic -r /mnt/backup/restic snapshots
restic -r /mnt/backup/restic check
```

**Borg:**

```bash
borg create --stats --compression lz4 ssh://backup@nas01.example.com/backups/borg::'{now}' /etc /srv
borg list ssh://backup@nas01.example.com/backups/borg
borg check ssh://backup@nas01.example.com/backups/borg
```

Verify that the snapshot size is reasonable (deduplication working) and that `check` reports no errors.

### Stage 4 — Automate daily backups

- [ ] Create a small script that performs the backup and writes a log
- [ ] Run it from a systemd timer (daily or as needed)
- [ ] Include pruning (retention) in the same job

Example systemd timer for restic:

```ini
# /etc/systemd/system/backup.timer
[Unit]
Description=Daily restic backup

[Timer]
OnCalendar=*-*-* 02:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

```ini
# /etc/systemd/system/backup.service
[Unit]
Description=Daily restic backup
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/backup-restic.sh
```

The script itself:

```bash
#!/usr/bin/env bash
set -euo pipefail
export RESTIC_REPOSITORY=/mnt/backup/restic
export RESTIC_PASSWORD_FILE=/root/.restic-pass

restic backup /etc /srv --exclude-caches
# retention: keep 7 daily, 5 weekly, 12 monthly, 2 yearly
restic forget --keep-daily 7 --keep-weekly 5 --keep-monthly 12 --keep-yearly 2 --prune
restic check --with-cache >> /var/log/restic.log 2>&1
```

For Borg, the equivalent uses `borg prune --keep-daily 7 --keep-weekly 4 --keep-monthly 6 --keep-yearly 1`.

Then:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now backup.timer
sudo systemctl list-timers backup.timer
```

### Stage 5 — Offsite copy

- [ ] If using restic, point a second copy at S3-compatible storage or another host
- [ ] With Borg, run a second `borg create` at a different location, or use `rclone sync` of the repository
- [ ] Enforce encryption at rest on the target and rotate keys sensibly

S3 example (restic):

```bash
export AWS_ACCESS_KEY_ID=...
export AWS_SECRET_ACCESS_KEY=...
restic -r s3:s3.example.com/bucket/restic init
restic -r s3:s3.example.com/bucket/restic backup /etc /srv
```

### Stage 6 — Test restore, document the procedure

- [ ] Do a real restore of one directory or one Docker volume to a temporary path
- [ ] Verify the restored data is complete and usable
- [ ] Write down the restore commands in a `RESTORE.md` next to the backup scripts, including the repository password location

**restic restore:**

```bash
# find the snapshot id
restic -r /mnt/backup/restic snapshots
# restore the whole snapshot to /tmp/restore
restic -r /mnt/backup/restic restore latest --target /tmp/restore
# or restore a single path
restic -r /mnt/backup/restic restore latest --include /etc/nginx --target /tmp/restore
```

**Borg restore:**

```bash
borg extract ssh://backup@nas01.example.com/backups/borg::backup-2026-10-07T02:00 --path etc/nginx
# or mount and inspect:
borg mount ssh://backup@nas01.example.com/backups/borg::backup-2026-10-07T02:00 /mnt/borg-view
```

## Verification

- [ ] `restic snapshots` / `borg list` shows fresh daily snapshots
- [ ] Server logs show no errors for the last week
- [ ] A restore to a scratch directory succeeded and data opened correctly
- [ ] The offsite repository contains an up-to-date copy
- [ ] Retention is working: old snapshots are pruned

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Backup fails at night | Timer ran before network was up | Add `After=network-online.target` + `Wants=network-online.target` |
| Repo password forgotten | No password manager | Store passphrase in a password manager and physically sealed copy before going live |
| Snapshots growing unbounded | No `forget`/`prune` in cron | Add retention pruning to the backup job |
| `check` reports errors | Disk corruption or concurrent access | Restore from last good snapshot; investigate storage hardware |
| Backup too slow / too large | No exclusions for caches/temp | Add `--exclude-caches`, exclude `/proc`, `/sys`, caches |

## Related pages

- [Restic](../storage/backup/restic.md)
- [BorgBackup](../storage/backup/borgbackup.md)
- [Duplicacy and Alternatives](../storage/backup/index.md)
- [ZFS and Btrfs Snapshots](../storage/backup/index.md)
- [Rclone (transport)](../storage/backup/rclone.md)