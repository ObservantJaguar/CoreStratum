---
title: Make
parent: Build Systems and Compilers
---

# Make

Make is the traditional build automation utility that orchestrates compilation by reading rules defined in a Makefile. It tracks file dependencies by comparing timestamps and rebuilds only the targets whose inputs have changed, making incremental builds efficient.

Despite its age, Make remains widely used and is a learning stepping stone for build tooling. GNU Make is the standard implementation on Linux systems and is frequently used as a top-level orchestrator wrapping other build systems.

## Resources

- [Official documentation (GNU Make manual)](https://www.gnu.org/software/make/manual/)
- [Official website](https://www.gnu.org/software/make/)