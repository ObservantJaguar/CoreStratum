---
title: Strace
parent: Debugging and Profiling
---

# Strace

Strace is a diagnostic tool for Linux that intercepts and records system calls made by a running process, along with their arguments and return values. It reveals exactly how a program interacts with the operating system kernel, including file access, networking, signals and process management.

It is invaluable for troubleshooting missing files, permission errors, unexpected network activity and application startup failures without modifying or recompiling the program.

## Resources

- [Official manual (Linux man pages)](https://man7.org/linux/man-pages/man1/strace.1.html)
- [Official repository](https://strace.io)