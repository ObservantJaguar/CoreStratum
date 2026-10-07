---
grand_parent: Practice
title: Matrix Messenger
parent: Guides
---

# Matrix Messenger

## Goal

A fully self-hosted corporate messenger based on **Matrix**: private rooms and direct messages, end-to-end encryption by default, file sharing, and **audio/video calls** between desktop and mobile clients. The stack is **Synapse** (homeserver), **Element** (web and mobile clients) and **coturn** (TURN server for calls). Optionally you can enable bridges to Telegram or Slack, and federation with other Matrix servers.

This is the recommended messenger for most SMB teams because Matrix is the only fully open protocol that provides reliable group calls and excellent clients in 2026.

## Scope and out of scope

**In scope:**
- Synapse homeserver (Docker, behind the Traefik foundation layer)
- Element Web as the primary client
- coturn for NAT traversal in audio/video calls
- User management, basic policies (registration, federation)
- Backups of Synapse's database and media store

**Out of scope:**
- Bridges (Telegram/Slack/WhatsApp) — mentioned in the roadmap as an extension
- Full federation tuning and room-version politics
- High-availability clusters (single-server setup)

## Prerequisites

- A Linux server (can be the [Docker Host with Traefik](docker-host-traefik.md) foundation)
- Domain with `matrix.example.com` (client-server API) and (recommended) `element.example.com` for the web client
- Ports 80/443 open for the API and web client
- Port **8448** reachable from outside if you enable federation
- A TURN port range (e.g. 3478 and udp 49152-65535) open for calls

## Architecture

```
                    РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’
  Element Web/App РІвЂќР‚РІвЂќР‚РІвЂ“С”РІвЂќвЂљ  Synapse  (matrix.example.com:443/8448)РІвЂќвЂљ
   (encrypted HTTP)  РІвЂќвЂљ   РІвЂ“С‘ PostgreSQL (SQLite ok for 5-10)    РІвЂќвЂљ
      РІвЂќвЂљ              РІвЂќвЂљ   РІвЂ“С‘ media store  (/var/lib/synapse)    РІвЂќвЂљ
      РІвЂќвЂљ      UDP     РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ¬РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ
      РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂ“С” coturn (TURN/STUN)      РІвЂќвЂљ
            3478 / 49152-65535       РІвЂ“С
                            (calls relayed if NAT)
```

## Roadmap

### Stage 1 — Prepare the foundation

- [ ] Follow the [Docker Host with Traefik](docker-host-traefik.md) guide if not already done
- [ ] Create `matrix` folder: `sudo mkdir -p /opt/containers/matrix`
- [ ] DNS: `matrix.example.com` and `element.example.com` point at the server

### Stage 2 — Generate Synapse config

Generate the homeserver configuration with the official image:

```bash
docker run --rm -v /opt/containers/matrix/data:/data \
  -e SYNAPSE_SERVER_NAME=matrix.example.com \
  -e SYNAPSE_REPORT_STATS=no \
  synapseorg/synapse:latest generate
```

This creates `homeserver.yaml` under `data/`.

- [ ] Review `data/homeserver.yaml`
- [ ] Set `enable_registration: false` after creating your users (or enable with a token for self-signup)
- [ ] Set `server_name: matrix.example.com`
- [ ] Note the `registration_shared_secret` for running `register_new_matrix_user`

### Stage 3 — Add PostgreSQL (recommended)

- [ ] Add a `postgres` service to the compose file (or use SQLite for a small team)
- [ ] Create the database and user for Synapse

```bash
docker compose exec db psql -U synapse -c "CREATE DATABASE synapse ENCODING 'UTF8';"
```

Point `database:` in `homeserver.yaml` at the container service; restart Synapse and verify `psql` connectivity.

### Stage 4 — Deploy Synapse behind Traefik

Create `/opt/containers/matrix/docker-compose.yml`:

```yaml
services:
  synapse:
    image: synapseorg/synapse:latest
    container_name: synapse
    restart: unless-stopped
    volumes:
      - ./data:/data
    networks:
      - proxy
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.matrix.rule=Host(`matrix.example.com`)"
      - "traefik.http.routers.matrix.entrypoints=websecure"
      - "traefik.http.routers.matrix.tls.certresolver=letsencrypt"
      - "traefik.http.services.matrix.loadbalancer.server.port=8008"

networks:
  proxy:
    external: true
```

- [ ] `docker compose up -d`
- [ ] Check logs: `docker compose logs -f synapse`
- [ ] Confirm `https://matrix.example.com/_matrix/client/versions` returns JSON

### Stage 5 — Create users

```bash
docker exec -it synapse register_new_matrix_user \
  -c /data/homeserver.yaml http://localhost:8008
```

- [ ] Create `admin` account and at least one test user
- [ ] Log in with both via Element

### Stage 6 — Element Web

- [ ] Deploy Element Web as a static site (simplest: official image) behind Traefik
- [ ] Point it at your homeserver URL

```yaml
services:
  element:
    image: vectorim/element-web:latest
    container_name: element
    restart: unless-stopped
    networks:
      - proxy
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.element.rule=Host(`element.example.com`)"
      - "traefik.http.routers.element.entrypoints=websecure"
      - "traefik.http.routers.element.tls.certresolver=letsencrypt"
      - "traefik.http.services.element.loadbalancer.server.port=80"
```

Element Web auto-discovers your server from the `/.well-known/matrix/client` record. Add that JSON response on a web server you control (for example Traefik on `element.example.com`):

```json
{ "m.homeserver": { "base_url": "https://matrix.example.com" } }
```

### Stage 7 — coturn for voice and video

- [ ] Deploy **coturn** behind Traefik (TLS/TURNS) or directly
- [ ] Configure static auth secret shared with Synapse
- [ ] Open the TURN port range

```yaml
services:
  coturn:
    image: coturn/coturn:latest
    container_name: coturn
    restart: unless-stopped
    command: >
      -n --log-file=stdout
      --lt-cred-mech --fingerprint --no-multicast-peers
      --realm=example.com
      --static-auth-secret=CHANGE_ME_SECRET
      --listening-port=3478
      --min-port=49152 --max-port=65535
    ports:
      - "3478:3478/udp"
      - "49152-65535:49152-65535/udp"
```

In `homeserver.yaml` set `turn_uris: ["turn:turn.example.com:3478?transport=udp"]`, `turn_shared_secret:` and `turn_allow_guests: false`, then restart Synapse.

- [ ] After this, calls should connect even between users behind strict NAT

### Stage 8 — Backups

- [ ] Back up the PostgreSQL database (dump nightly)
- [ ] Back up the media store directory
- [ ] Wire it into the [Backup with restic and Borg](backup-restic-borg.md) guide

### Stage 9 — (Optional) Bridges and federation

**Federation:** if enabled, Synapse federates with other Matrix servers over port 8448. If you want a purely corporate (walled-garden) messenger, keep `enable_registration: false` and consider blocking federation, or leave federation on but restrict who can join rooms.

**Bridges** (e.g. Telegram) run as separate containers connected to the same network. The mautrix-* bridge family is the most maintained:

- [mautrix-telegram](https://github.com/mautrix/telegram)

## Verification

- [ ] `https://matrix.example.com/_matrix/client/versions` returns valid JSON
- [ ] Two test users can create a private room and exchange encrypted messages
- [ ] E2E keys are verified in Element (green shield)
- [ ] A voice call between two devices works (including across a NAT)
- [ ] Element loads via `https://element.example.com` and connects to your homeserver
- [ ] `docker compose logs` shows clean TURN usage during a call
- [ ] After a restart, users can still log in and access history (DB + media intact)

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Element can't connect | `.well-known` or homeserver URL wrong | Check `/_matrix/client/versions` and the Well-Known JSON |
| Calls fail between two users | coturn not deployed or port range closed | Verify UDP 3478 + 49152-65535 open; check `turn_shared_secret` matches |
| Federation broken | Port 8448 not reachable | Open 8448; verify with `matrix.org/federation-tester` |
| Registration enabled publicly | `enable_registration: true` | Set `false` now; create users via `register_new_matrix_user` |
| Media upload fails | Media store not writable or full | Check `data/media_store` permissions/disk space |
| URL previews don't work | Missing `url_preview` settings | Enable `url_preview_*` in homeserver.yaml and allow the range |

## Related pages

- [Synapse](../communications/messaging/synapse.md)
- [Dendrite and Conduit (alternative servers)](../communications/messaging/dendrite.md)
- [Element](../communications/messaging/element.md)
- [coturn](../communications/messaging/coturn.md)
- [Docker Host with Traefik](docker-host-traefik.md)
- [Backup with restic and Borg](backup-restic-borg.md)