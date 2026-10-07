---
title: Image Builders
parent: Containers and Runtimes
grand_parent: Tools
---

# Image Builders

Image builders are tools that assemble container images from a description of their contents, typically a Dockerfile or equivalent build script. The image builder resolves the base layers, applies the steps and exports a standard OCI image that can be stored in a registry and run by any conforming runtime.

Unlike engines, image builders focus solely on producing images rather than running containers. Building is often done separately so that images can be assembled without the privileges or daemons required to run them.

## Tools

- [Buildah](buildah.md)