---
title: Nomad
parent: Cluster Schedulers
---

# Nomad

Nomad, from HashiCorp, is a flexible cluster scheduler that places and manages workloads across a fleet of machines. Unlike Kubernetes, it schedules not only containers but also standalone binaries, Java applications and even virtual machines, using a simple binary-based agent model.

Nomad is designed to be easy to operate, integrates with HashiCorp Consul for service discovery and supports a range of task drivers, making it a good fit for mixed or simpler workloads.

## Notes for administrators

- Single-server and multi-region deployment with a small operational surface.
- Schedules containers (Docker, containerd) as well as raw executables and VMs.
- Combines well with Consul and Vault for a full HashiCorp stack.

## Resources

- [Nomad documentation](https://developer.hashicorp.com/nomad)
- [Nomad on GitHub](https://github.com/hashicorp/nomad)
- [Nomad Jobs specification](https://developer.hashicorp.com/nomad/docs/job-specification)