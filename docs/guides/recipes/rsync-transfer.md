---
title: Move a Directory Between Servers with rsync
parent: Recipes
grand_parent: Guides
---

# Move a Directory Between Servers with rsync

## Goal

Copy a directory from server A to server B once and keep it in sync, preserving permissions and ownership.

## Task

Move `/srv/data` from server A to server B, keeping file permissions/ownership and transferring incrementally.

## Steps

1. Dry run first to preview what would be transferred (no changes):

```bash
rsync -avz --dry-run /srv/data/ user@B.example.com:/srv/data/
```

2. Run the real transfer with archive + compression + deletion:

```bash
rsync -avz --delete /srv/data/ user@B.example.com:/srv/data/
```

3. For flaky links, resume partial files on the next run:

```bash
rsync -avz --partial /srv/data/ user@B.example.com:/srv/data/
```

4. Repeat the same command periodically to keep B in sync incrementally.

## Verification

- A second dry run reports nothing left to do:

```bash
rsync -av --dry-run /srv/data/ user@B.example.com:/srv/data/
```

shows `0 files` / no files listed.

- Checksums match on both sides:

```bash
cd /srv/data && find . -type f -exec md5sum {} + | sort > /tmp/a.md5
ssh user@B 'cd /srv/data && find . -type f -exec md5sum {} + | sort' > /tmp/b.md5
diff /tmp/a.md5 /tmp/b.md5
```

## Gotchas

- **`--delete` removes extra files on the receiver** - report well; you can wipe files that only exist on B. Always dry run first and understand the source/destination before enabling it.
- **Trailing slash semantics** - `/srv/data/` (with slash) copies the *contents* of `data` into the destination; `/srv/data` (no slash) copies the `data` *directory itself*. Pick deliberately.
- **Ownership/permissions** - `-a` preserves them, but writing as an unprivileged user cannot set original UIDs/GIDs. Run as root or add `-o` / `-g` to allow ownership changes.
- **First sync is slow** - the initial full transfer, especially over a WAN, can take a long time; use `--partial` and restartable batches (`--info=progress2`) rather than restarting from zero.

## Related

- [Backup overview](../../storage/backup/index.md)
- [File transfer over SSH](../../foundations/protocols/index.md)