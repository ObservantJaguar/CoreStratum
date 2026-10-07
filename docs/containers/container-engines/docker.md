---
title: Docker
parent: Container Engines
---

# Docker

Docker is the de-facto standard tool for automating the deployment and management of applications inside containers. It packages an application together with all its settings and dependencies into a portable container image that runs consistently on any system.

## Key concepts

- **Images** — read-only templates from which containers are started.
- **Containers** — running instances created from an image.
- **Dockerfile** — a script describing how to assemble an image.
- **Docker Hub / registries** — repositories for publishing and pulling images.
- **Docker Compose** — a tool for defining and running multi-container applications.
- **Docker Engine** — the client-server application (daemon) that builds and runs containers.

## Notes for administrators

- Supports Linux, Windows and macOS environments.
- Containers share the host kernel; isolation is provided by Linux namespaces and cgroups.
- Used as the basis for many CI/CD pipelines and local development setups.

## Resources

- [Official documentation](https://docs.docker.com)
- [Docker Engine on GitHub](https://github.com/moby/moby)
- [Getting-started tutorial](https://docs.docker.com/get-started/)