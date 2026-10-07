---
grand_parent: Practice
title: Git Server with Gitea
parent: Guides
---

# Git Server with Gitea

## Goal

A self-hosted Git hosting platform for a small team: repositories with access control, issues, pull requests, built-in CI/CD (Actions), container registry and a lightweight resource footprint. The platform is **Gitea** (or its fully community-governed fork **Forgejo**).

By the end, developers use `git push` to a server under your control, review changes in the web UI, and can run simple CI pipelines — with backups.

## Scope and out of scope

**In scope:**
- Gitea deployment (Docker, behind Traefik)
- HTTPS/TLS, LDAP/OAuth login (optional), 2FA
- Access control (teams, repos, branches)
- Actions (built-in CI) basics
- Mirroring, backup and restore

**Out of scope:**
- Full GitLab replacement (heavy features; see [GitLab](../development/version-control/gitlab.md) if needed)
- Kubernetes-based deployment
- Code intelligence/SAST at scale

## Prerequisites

- The [Docker Host with Traefik](docker-host-traefik.md) foundation layer
- Domain: `git.example.com`
- Storage for repositories (SSD preferred)

## Architecture

```
   developers ----(git over https)----> Traefik ---> Gitea (container)
   developers ----(web UI)-------------> Traefik ---> Gitea
        |
        +------ SQLite (default) or PostgreSQL (many users)
        +------ Actions runner (CI) -- on the host, connected to Gitea
        +------ restic/Borg backup of repos + DB
```

## Roadmap

### Stage 1 — Deploy Gitea

Create `/opt/containers/gitea/docker-compose.yml` (PostgreSQL option shown):

```yaml
services:
  db:
    image: postgres:16-alpine
    restart: unless-stopped
    environment:
      POSTGRES_USER: gitea
      POSTGRES_PASSWORD: CHANGE_ME_DB
      POSTGRES_DB: gitea
    volumes: ["./db:/var/lib/postgresql/data"]
    networks: [proxy]

  gitea:
    image: gitea/gitea:latest
    restart: unless-stopped
    depends_on: [db]
    environment:
      GITEA__database__DB_TYPE: postgres
      GITEA__database__HOST: db:5432
      GITEA__database__NAME: gitea
      GITEA__database__USER: gitea
      GITEA__database__PASSWD: CHANGE_ME_DB
      GITEA__server__ROOT_URL: "https://git.example.com/"
      GITEA__server__DOMAIN: git.example.com
      GITEA__server__SSH_DOMAIN: git.example.com
      GITEA__server__SSH_PORT: "2222"
    volumes:
      - "./data:/data"
      - "/etc/timezone:/etc/timezone:ro"
      - "/etc/localtime:/etc/localtime:ro"
    ports:
      - "2222:22"      # SSH access to repos
    networks: [proxy]
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.gitea.rule=Host(`git.example.com`)"
      - "traefik.http.routers.gitea.entrypoints=websecure"
      - "traefik.http.routers.gitea.tls.certresolver=letsencrypt"
      - "traefik.http.services.gitea.loadbalancer.server.port=3000"

networks:
  proxy:
    external: true
```

- [ ] Start the stack and open https://git.example.com
- [ ] Complete the install screen (database, admin account)
- [ ] Register an admin and a test user

### Stage 2 — SSH access

- [ ] The host port 2222 forwards to Gitea's SSH (port 22 inside the container)
- [ ] Users add their SSH key in the web UI at **Settings �� ’ SSH Keys**
- [ ] Test `git clone ssh://git@git.example.com:2222/org/repo.git`

### Stage 3 — Access control

- [ ] Create an **organization** and **teams** (Owners, Developers, Viewers)
- [ ] Set repository visibility (private/public) per project
- [ ] Protect `main` branch (require PR review) on important repos
- [ ] Enable 2FA for admins (Gitea supports TOTP)

### Stage 4 — CI/CD with Actions

- [ ] Enable Actions in the admin/org settings
- [ ] Register an Actions runner on a host (`act_runner`) that connects to Gitea
- [ ] Create a `.gitea/workflows/ci.yml` in a repo

Simple workflow:

```yaml
name: CI
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: make test
```

- [ ] Push a commit; verify the pipeline runs and reports green/red in the UI

### Stage 5 — Backups

- [ ] Back up the `data/` directory (repos, SSH keys, config) nightly
- [ ] Back up the PostgreSQL database (or SQLite file)
- [ ] Use the built-in `gitea dump` command where possible
- [ ] Include in the [Backup with restic and Borg](backup-restic-borg.md) pipeline

```bash
docker exec -u git gitea gitea dump -c /data/gitea/conf/app.ini
```

### Stage 6 — Optional: LDAP/OAuth login

- [ ] In Admin �� ’ Authentication sources, add LDAP (if you have FreeIPA/Samba) or OAuth (e.g. Keycloak)
- [ ] Test login with an LDAP account
- [ ] If no directory server, skip — local accounts are fine for small teams

## Verification

- [ ] Register and log in at https://git.example.com
- [ ] `git clone` over SSH works from a developer machine
- [ ] Create a PR between branches; merge with protected-branch restriction
- [ ] An Actions run executes a workflow and shows success
- [ ] After a restore from backup, repos, users and CI config return

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Git over SSH fails | Host port 2222 not open or wrong key | Open 2222; check `GITEA__server__SSH_PORT` and firewall |
| Web UI slow | SQLite vs Postgres choice | Switch to Postgres for more than a few users |
| Actions runner offline | Runner not registered or token wrong | Re-register `act_runner` with current token from Settings �� ’ Actions |
| Clone URL wrong | `ROOT_URL`/`DOMAIN` misconfigured | Set `GITEA__server__ROOT_URL=https://git.example.com/` |
| Backup missing new repos | Backup not including `data/` | Back up full `data/` volume (repos live there) |

## Related pages

- [Gitea](../development/version-control/gitea.md)
- [Forgejo (community fork)](../development/version-control/forgejo.md)
- [Git](../development/version-control/git.md)
- [Docker Host with Traefik guide](docker-host-traefik.md)
- [Backup with restic and Borg guide](backup-restic-borg.md)