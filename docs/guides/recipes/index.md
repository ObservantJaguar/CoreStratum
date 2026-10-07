---
title: Recipes
parent: Guides
nav_order: 1
has_children: true
---

# Recipes

Short, single-purpose recipes for everyday IT tasks - the opposite of the long roadmaps. Each recipe answers one concrete question ("how do I set up SSH key auth?", "how do I add a firewall rule?") in a few steps plus a verification check.

## Structure of a recipe

1. **Goal** - one line: what you get.
2. **Task** - the concrete need.
3. **Steps** - 3-7 concrete commands/config.
4. **Verification** - how to confirm it worked.
5. **Gotchas** - common mistakes.

## Recipes

- [SSH Key-Based Authentication](ssh-key-auth.md)
- [Add a Firewall Rule (nftables/iptables)](firewall-rule.md)
- [Create and Restore a Logical Volume (LVM)](lvm-create-restore.md)
- [Schedule a Task with cron/systemd-timer](cron-systemd-timer.md)
- [Diagnose DNS Resolution Problems](dns-diagnostics.md)
- [Force a Kubernetes Pod Rollout](k8s-rollout.md)
- [Encrypt a Disk Partiton/LUKS](luks-setup.md)
- [Generate and Trust a Self-Signed Certificate](selfsigned-cert.md)
- [Move a Directory Between Servers with rsync](rsync-transfer.md)
- [Take a Quick Snapshot with btrfs/ZFS](snapshot-quick.md)