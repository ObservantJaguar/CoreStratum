---
title: Valgrind
parent: Debugging and Profiling
---

# Valgrind

Valgrind is a framework of instrumentation tools for dynamically analyzing programs. Its most famous tool, Memcheck, detects memory leaks, invalid memory access, use of uninitialized memory and other common C/C++ memory errors that can otherwise cause undefined behavior.

Beyond memory checking, Valgrind provides tools for cache and branch profiling (Cachegrind), heap profiling (Massif), thread error detection (Helgrind) and call-graph profiling. It is essential for verifying correctness and performance of native applications.

## Resources

- [Official documentation](https://valgrind.org/docs/manual/manual.html)
- [Official website](https://valgrind.org)