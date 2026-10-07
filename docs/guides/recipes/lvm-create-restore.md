---
title: Create and Restore a Logical Volume (LVM)
parent: Recipes
grand_parent: Guides
---

# Create and Restore a Logical Volume (LVM)

## Goal

Create a mountable LVM logical volume on a new disk, and restore it after a reinstall or re-attach.

## Task

Turn a new raw disk (`/dev/sdb`) into an LVM volume group with a 100&nbsp;GiB logical volume mounted at `/data`, and known how to restore the setup (re-attach/reload) afterwards.

## Steps

1. Initialize the disk as a physical volume (PV):

```bash
sudo pvcreate /dev/sdb
```

2. Create a volume group (VG) on the PV:

```bash
sudo vgcreate data_vg /dev/sdb
```

3. Create a logical volume (LV) of 100&nbsp;GiB:

```bash
sudo lvcreate -L 100G -n data_lv data_vg
```

4. Format and mount it:

```bash
sudo mkfs.ext4 /dev/data_vg/data_lv
sudo mkdir -p /data
sudo mount /dev/data_vg/data_lv /data
```

5. Persist the mount in `/etc/fstab` using the filesystem UUID (not the device name, which can change):

```bash
blkid /dev/data_vg/data_lv
echo 'UUID=<uuid> /data ext4 defaults 0 2' | sudo tee -a /etc/fstab
```

6. Restore/re-activate an existing volume group (e.g. after the disk was unplugged or on a reinstall):

```bash
sudo vgscan
sudo vgchange -ay
sudo mount /data
```

## Verification

- The LV is mounted:

```bash
mount | grep data
df -h /data
```

- The VG/LV is visible:

```bash
sudo pvs; sudo vgs; sudo lvs
```

- After a reboot the volume mounts automatically with no error.

## Gotchas

- **Back up the UUID** - `blkid` output is what `/etc/fstab` needs. If you write a wrong UUID into fstab the system may fail to boot; keep a copy of `blkid` output and use `systemctl reset-failed` / recovery shell to fix it.
- **Enlarging later is easy** - when the LV fills up: `sudo lvextend -L +50G /dev/data_vg/data_lv` then `sudo resize2fs /dev/data_vg/data_lv` (online, no unmount needed for ext4).
- **`/dev/sdX` names are not stable across reboots** - always address the LV through `/dev/data_vg/data_lv` or the UUID, never a raw `/dev/sdb` path in fstab.
- **Restoring a snapshot** - if you snapshot an LV, `lvconvert --merge` an LVM snapshot to return to a previous state.

## Related

- [Storage overview](../../storage/block/lvm.md)
- [Disk encryption (LUKS)](luks-setup.md)