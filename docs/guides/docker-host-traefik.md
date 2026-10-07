---
grand_parent: Practice
title: Docker Host with Traefik
parent: Guides
---

# Docker Host with Traefik

## Goal

A single Linux server that runs Docker containers behind the **Traefik** reverse proxy with **automatic HTTPS** (Let's Encrypt). After this guide you can deploy any web service (Nextcloud, Matrix, Gitea, monitoring dashboards...) as a container, give it a hostname such as `nextcloud.example.com`, and Traefik will route traffic and obtain and renew TLS certificates automatically.

This is the **foundation layer**: most of the other guides in this section assume that this base is in place.

## Scope and out of scope

**In scope:**
- Docker Engine installation and configuration
- Traefik v3 as the reverse proxy for all container traffic
- Automatic TLS certificates via Let's Encrypt (ACME)
- Secure access to the admin dashboard
- A basic, secure layout that other services can extend

**Out of scope:**
- Hardening of the host OS itself (see [Hardening and MAC](../security/hardening/index.md))
- Kubernetes or Swarm clustering (this guide is a single host)
- Load balancing across multiple hosts

## Prerequisites

- A Linux server (Debian or Ubuntu are assumed here; the steps translate to other distributions).
- A public DNS domain (or a subdomain) pointing to the server's IP.
- Ports **80** and **443** reachable from the internet.
- Basic comfort with the shell, systemd and text editors.

## Architecture

```
                         Internet
                             |
                        (80/443)
                             |
      +--------------------------+
      |         Traefik          |   reverse proxy + automatic TLS
      |        (container)       |
      +--------------------------+
                             |
           +-----------------+-----------------+
           |                 |                 |
    +-------------+   +-------------+   +-------------+
    | service A   |   | service B   |   | service C   |    (containers)
    | nextcloud   |   |   gitea     |   |   matrix     |
    +-------------+   +-------------+   +-------------+

Everything shares one Docker network. Services publish no ports to the
host; Traefik reaches them over the internal network and terminates TLS.
```

## Roadmap

### Stage 1 — Prepare the host

- [ ] Update the OS and install base utilities
- [ ] Set a correct hostname and time zone
- [ ] Create a dedicated user for Docker management (optional but recommended)
- [ ] Configure a firewall so only ports 22, 80 and 443 are open

For Debian/Ubuntu:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl ca-certificates gnupg lsb-release ufw
sudo hostnamectl set-hostname docker-01
sudo timedatectl set-timezone Europe/Moscow
sudo ufw allow 22/tcp && sudo ufw allow 80/tcp && sudo ufw allow 443/tcp
sudo ufw enable
```

### Stage 2 — Install Docker Engine

- [ ] Install Docker from the official repository
- [ ] Enable and start the Docker service
- [ ] Add your user to the `docker` group

```bash
curl -fsSL https://get.docker.com | sudo sh
sudo systemctl enable --now docker
sudo usermod -aG docker "$USER"
```

Log out and back in (or run `newgrp docker`) so the group change takes effect.

### Stage 3 — Project layout

- [ ] Decide on a home directory for the stack (for example `/opt/containers`)
- [ ] Create one folder per service, each with its own `docker-compose.yml`
- [ ] Create a shared external Docker network for all services

```bash
sudo mkdir -p /opt/containers
docker network create proxy
```

The external `proxy` network is **shared** — every service that should be published through Traefik joins this network.

### Stage 4 — Deploy Traefik

- [ ] Create `/opt/containers/traefik/` with `docker-compose.yml` and config
- [ ] Enable the Docker provider and the ACME (Let's Encrypt) resolver
- [ ] Protect the dashboard with HTTP Basic Auth
- [ ] Start Traefik and check the logs

```yaml
# /opt/containers/traefik/docker-compose.yml
services:
  traefik:
    image: traefik:v3.1
    container_name: traefik
    restart: unless-stopped
    command:
      - "--api.dashboard=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entrypoints.web.address=:80"
      - "--entrypoints.websecure.address=:443"
      - "--certificatesresolvers.letsencrypt.acme.tlschallenge=true"
      - "--certificatesresolvers.letsencrypt.acme.email=admin@example.com"
      - "--certificatesresolvers.letsencrypt.acme.storage=/letsencrypt/acme.json"
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock:ro"
      - "./letsencrypt:/letsencrypt"
    networks:
      - proxy
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.dashboard.rule=Host(`traefik.example.com`)"
      - "traefik.http.routers.dashboard.service=api@internal"
      - "traefik.http.routers.dashboard.middlewares=auth"
      - "traefik.http.middlewares.auth.basicauth.users=admin:$$2y$$05$$...hash..."

networks:
  proxy:
    external: true
```

Notes:
- Replace `admin@example.com` and the domain in the dashboard router rule.
- The Basic Auth hash is generated with `htpasswd -nb admin 'verysecret'`.
- Set the email and check the Let's Encrypt rate limits before going live.

### Stage 5 — Start Traefik and verify

- [ ] Start the stack: `docker compose up -d`
- [ ] Check logs: `docker compose logs -f traefik`
- [ ] Open `https://traefik.example.com` and confirm the HTTPS certificate and dashboard

### Stage 6 — Publish a first test service

- [ ] Deploy a trivial container (for example `whoami`) with a Traefik label
- [ ] Verify routing and certificate through the browser

```yaml
services:
  whoami:
    image: containous/whoami
    networks:
      - proxy
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.whoami.rule=Host(`whoami.example.com`)"
      - "traefik.http.routers.whoami.entrypoints=websecure"
      - "traefik.http.routers.whoami.tls.certresolver=letsencrypt"

networks:
  proxy:
    external: true
```

## Verification

- [ ] `docker ps` shows Traefik running and healthy
- [ ] `https://whoami.example.com` returns the whoami page over TLS
- [ ] `https://traefik.example.com` opens the dashboard (requires auth)
- [ ] A broken container fails over cleanly (Traefik returns 502 or 503, no crash)

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Certificate not issued | Wrong DNS record or port 80 closed | Check `dig mx`/`A` record and firewall; see Traefik logs |
| Dashboard 404 | Router rule domain mismatch or `api@internal` misconfigured | Verify the `Host(...)` rule and that `--api.dashboard=true` is set |
| 401 on dashboard | Wrong Basic Auth hash | Regenerate with `htpasswd` and escape `$` as `$$` in Compose |
| Service unreachable | Service not on the `proxy` network | Add the `external: true` network to the service's Compose file |

## Related pages

- [Docker](../containers/container-engines/docker.md)
- [Traefik](../networking/load-balancing/traefik.md)
- [Nginx and Caddy (alternatives)](../communications/web/index.md)