---
title: System Containers
parent: Containers and Runtimes
grand_parent: Tools
---

# System Containers

System containers are a class of container that runs a full operating system distribution — with its own init, package manager and services — rather than a single application process. They behave much like lightweight virtual machines, but share the host kernel.

System containers provide a convenient way to run entire distributions in isolation, combining the resource efficiency of containers with the familiar administration of a real system.

- [LXC](lxc.md) — foundation of Linux system containers.
- [LXD](lxd.md) — container and VM manager built on LXC.
- [Proxmox VE](proxmox-ve.md) — platform integrating VMs and LXC containers.
- [systemd-nspawn](systemd-nspawn.md) — systemd-native namespace containers.