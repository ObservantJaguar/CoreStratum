---
title: Podman
parent: Container Engines
---

# Podman

Podman is a container engine that provides a Docker-compatible command-line interface without a central daemon. It runs containers in unprivileged user-space processes, which improves security and simplifies management, especially on rootless and pod-based workflows.

It is part of the containers ecosystem and integrates with the same OCI standards as Docker, so Podman and Docker can work side by side and even participate in the same registries.

## Notes for administrators

- Daemonless, so there is no background service to run as a privileged root process.
- Native support for pods, making the transition from Kubernetes concepts easier.
- Supports rootless containers, letting unprivileged users run containers securely.

## Resources

- [Podman documentation](https://podman.io)
- [Podman on GitHub](https://github.com/containers/podman)
- [Podman usage guides](https://docs.podman.io)