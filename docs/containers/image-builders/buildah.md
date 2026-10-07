---
title: Buildah
parent: Image Builders
---

# Buildah

Buildah is an open-source command-line tool for building Open Container Initiative (OCI) images without needing a container daemon or root privileges. It works directly with the filesystem, committing container layers into standard container images.

Because it separates building from running, Buildah is often paired with Podman and used in build environments where daemonless and rootless image construction is preferred.

## Notes for administrators

- Builds OCI and Docker-format images using existing container filesystems.
- Works without a daemon and supports running build steps in containers.
- Can create images directly from a Dockerfile or interactively from scratch.

## Resources

- [Buildah documentation](https://buildah.io)
- [Buildah on GitHub](https://github.com/containers/buildah)