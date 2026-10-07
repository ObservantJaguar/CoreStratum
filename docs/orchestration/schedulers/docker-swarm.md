---
title: Docker Swarm
parent: Cluster Schedulers
---

# Docker Swarm

Docker Swarm is the native, built-in clustering and scheduling feature of Docker Engine. It turns a group of Docker hosts into a single virtual host, letting you deploy services declaratively with built-in load balancing, service discovery and rolling updates.

For teams that already use Docker, Swarm offers a simple path to orchestration without learning a new platform, trading some of the power of Kubernetes for much lower operational complexity.

## Notes for administrators

- Built into Docker Engine, so there is no separate product to install.
- Uses the same Compose-style model, extended with a Swarm service definition.
- Supports rolling updates, scaling and encrypted overlay networks out of the box.

## Resources

- [Docker Swarm overview](https://docs.docker.com/engine/swarm/)
- [Docker Swarm mode concepts](https://docs.docker.com/engine/swarm/key-concepts/)
- [Docker on GitHub](https://github.com/docker)