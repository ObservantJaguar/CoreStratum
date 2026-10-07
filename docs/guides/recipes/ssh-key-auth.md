---
title: SSH Key-Based Authentication
parent: Recipes
grand_parent: Guides
---

# SSH Key-Based Authentication

## Goal

Log in to a Linux server without a password, using a public/private key pair, and disable password logins.

## Task

Set up `ssh-keygen` + `ssh-copy-id` on your workstation so that `ssh user@server` just works with a key.

## Steps

1. Generate a key pair on your workstation (if you don't have one):

```bash
ssh-keygen -t ed25519 -a 64
```

2. Copy the public key to the server:

```bash
ssh-copy-id user@server
```

3. Verify key login works:

```bash
ssh user@server
```

4. Disable password auth on the server (`/etc/ssh/sshd_config`):

```ini
PasswordAuthentication no
PubkeyAuthentication yes
```

5. Reload the SSH daemon:

```bash
sudo systemctl reload ssh
```

## Verification

- `ssh user@server` succeeds without asking for a password.
- A second terminal with `ssh -o PasswordAuthentication=no user@server` still logs in.

## Gotchas

- **Never close your current session before testing the new key** - you can lock yourself out. Test key login first, then disable passwords.
- Wrong permissions on `~/.ssh` break the key: `chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys`.
- The `root` user has `PermitRootLogin` separately - keep it `prohibit-password` if root key access is needed.
- On servers managed by Ansible/cloud-init, password auth is often already off; re-enable temporarily with `PasswordAuthentication yes` only during setup.

## Related

- [SSH and key concepts](../../foundations/protocols/index.md)
- [Hardening basics](../../security/hardening/index.md)