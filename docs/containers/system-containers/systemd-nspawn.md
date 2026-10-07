---
title: Docker in systemd-nspawn
parent: System Containers
---

# systemd-nspawn

systemd-nspawn is a tool for running a full Linux distribution or command in a light-weight namespace container, using the same kernel and featuring an init system managed by systemd. It can boot an entire OS tree with its own systemd as PID 1, resembling a containerized virtual machine.

It is a native systemd alternative to LXC for running system containers on machines already using systemd.

## Resources

- [Documentation](https://www.freedesktop.org/software/systemd/man/latest/systemd-nspawn.html)