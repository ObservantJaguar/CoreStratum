---
title: FreeBSD Jails
parent: Isolation Mechanisms
---

# FreeBSD Jails

FreeBSD jails are the historic OS-level virtualisation technology: an environment built around a directory tree that is granted very limited access to the rest of the system. Each jail has its own filesystem view, network stack, hostname and user set, running on the shared FreeBSD kernel.

Jails are a lightweight and mature way to run multiple isolated services or entire virtualised systems on one FreeBSD host with minimal overhead.

## Notes for administrators

- Basis of many commercial FreeBSD hosting and appliance products.
- Resource limits can be applied with `rctl` alongside jail confinement.
- Combine with ZFS to snapshot and replicate whole jail environments.

## Resources

- [FreeBSD Handbook: Jails](https://docs.freebsd.org/en/books/handbook/jails/)
- [freebsd-jail man page](https://man.freebsd.org/cgi/man.cgi?query=jail)
- [FreeBSD source on GitHub](https://github.com/freebsd/freebsd-src)