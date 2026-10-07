---
title: OverlayFS
parent: Linux Filesystems
---

# OverlayFS

OverlayFS is a union-mount filesystem in the Linux kernel that merges multiple directories into a single view. It is the foundation of container image layering, where a read-only lower layer is combined with a writable upper layer.

## Resources

- [OverlayFS documentation](https://docs.kernel.org/filesystems/overlayfs.html)