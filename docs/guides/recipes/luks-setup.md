---
title: Encrypt a Disk Partition/LUKS
parent: Recipes
grand_parent: Guides
---

# Encrypt a Disk Partition/LUKS

## Goal

Create a LUKS-encrypted partition and have it unlocked and mounted at boot.

## Task

Encrypt `/dev/sdb1` with LUKS and mount it at `/data` at boot.

## Steps

1. Wipe the partition and lay down a LUKS header (this destroys all data on it):

```bash
sudo cryptsetup luksFormat /dev/sdb1
```

Confirm with `YES` and set a strong passphrase.

2. Open the encrypted device under a mapper name:

```bash
sudo cryptsetup open /dev/sdb1 data_crypt
```

3. Format a filesystem on the now-decrypted layer:

```bash
sudo mkfs.ext4 /dev/mapper/data_crypt
```

4. Mount it manually to create data, then unmount for fstab setup:

```bash
sudo mount /dev/mapper/data_crypt /data
```

5. Add the device to `/etc/crypttab` so it is unlocked at boot (with a key file instead of prompting):

```ini
data_crypt /dev/sdb1 /etc/luks/data_crypt.key luks
```

Generate the key file, add it as a LUKS key slot, and restrict permissions:

```bash
sudo dd if=/dev/urandom of=/etc/luks/data_crypt.key bs=512 count=8
sudo chmod 600 /etc/luks/data_crypt.key
sudo cryptsetup luksAddKey /dev/sdb1 /etc/luks/data_crypt.key
```

6. Add the mapper device to `/etc/fstab`:

```bash
echo 'UUID=<uuid-of-mapper> /data ext4 defaults 0 2' | sudo tee -a /etc/fstab
```

Find the UUID with `blkid /dev/mapper/data_crypt`.

## Verification

- The encrypted device is visible as a mapper device:

```bash
lsblk
```

shows `data_crypt` on top of `sdb1`.

- The LUKS header is intact:

```bash
sudo cryptsetup luksDump /dev/sdb1
```

- After a reboot `/data` is mounted automatically.

## Gotchas

- **`luksFormat` destroys all data on the partition** - there is no undo. Double-check the device path and back up anything important first.
- **Back up the LUKS header** - losing the header (bad sector, overwrite) makes the data unrecoverable even with the passphrase. `sudo cryptsetup luksHeaderBackup /dev/sdb1 --header-backup-file /backup/data_crypt.hdr` and store it off that disk.
- **Losing the passphrase / key file = losing the data** - there is no recovery. Test unlock on a spare device or keep a second LUKS key slot (`luksAddKey`).
- **Do not reuse the same passphrase for root and data without a recovery path** - a single compromised passphrase exposes everything; for the root/boot volume plan a recovery mechanism (console initramfs, key file on USB) before relying on it.
- **`crypttab` vs `luks`** - the last field `luks` tells the initramfs to use LUKS and to look up the header; for a detached header or plain dm-crypt the options differ.

## Related

- [Disk encryption concepts](../../security/cryptography/luks.md)
- [LVM volumes](lvm-create-restore.md)
- [Disk management](../../storage/block/index.md)