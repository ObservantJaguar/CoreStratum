---
grand_parent: Practice
title: Nextcloud and CRM
parent: Guides
---

# Nextcloud and CRM

## Goal

A self-hosted **corporate file cloud** with document collaboration plus a **CRM** you own. The plan covers two workloads:

1. **Nextcloud Hub** — files, calendar, contacts, collaborative editing (via OnlyOffice or Collabora), Talk chat, and enterprise-grade access control. This is the document layer.
2. **A CRM** — choose **Odoo** (full ERP/CRM with inventory, invoicing, projects) or **EspoCRM** (lightweight, focused CRM). Both are open-source.

By the end, employees have a Dropbox/Google Drive + SharePoint-grade experience hosted entirely on your own servers, with an integrated CRM.

## Scope and out of scope

**In scope:**
- Nextcloud deployment (Docker, behind Traefik) with database (MariaDB/PostgreSQL)
- OnlyOffice (or Collabora) document server for live editing
- Nextcloud Talk optional (or advise Matrix instead)
- Odoo or EspoCRM deployment with their requirements
- Backup of app data and databases

**Out of scope:**
- Multi-node scaling
- Office suite migration tooling
- Advanced audit/compliance (basics covered)

## Prerequisites

- The [Docker Host with Traefik](docker-host-traefik.md) foundation layer
- Domain: `nextcloud.example.com`, `office.example.com` (document server), `crm.example.com`
- RAM/CPU: Nextcloud alone is light; OnlyOffice/Collabora wants 2+ GB RAM; Odoo wants 2РІР‚вЂњ4 GB. Plan a server with 8 GB RAM if you run all three.
- Storage: SSDs preferred for the database and media.

## Choosing the CRM

| | Odoo | EspoCRM |
|---|---|---|
| Scope | Full business suite (CRM, inventory, invoicing, projects, HR) | Focused CRM (leads, deals, email, workflow) |
| Complexity | Higher; needs modules, updates, maybe an expert | Lower; simple setup, lighter resource use |
| Best for | When you also need ERP/inventory/accounting | When CRM alone is the priority |
| License | LGPL (community edition) | AGPL |

Both are fine on one host. If in doubt, start with **EspoCRM** to keep the stack lean, and grow into Odoo later.

## Architecture

```
                       РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’
  users РІвЂќР‚РІвЂќР‚РІвЂ“С” Traefik РІвЂќР‚РІвЂќР‚РІвЂ“С”РІвЂќвЂљ Nextcloud (files, calendar, talk)РІвЂќвЂљ
                       РІвЂќвЂљ   РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂ“С” OnlyOffice/Collabora      РІвЂќвЂљ
                       РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ
                       РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’
  users РІвЂќР‚РІвЂќР‚РІвЂ“С” Traefik РІвЂќР‚РІвЂќР‚РІвЂ“С”РІвЂќвЂљ CRM: Odoo  OR  EspoCRM           РІвЂќвЂљ
                       РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ
                 Both share: the proxy network, a database,
                 and the restic/Borg backup pipeline.
```

## Roadmap

### Stage 1 — Nextcloud (core)

- [ ] Create `/opt/containers/nextcloud` with `docker-compose.yml`
- [ ] Add a database service (MariaDB) and a Redis service for performance
- [ ] Deploy Nextcloud behind Traefik
- [ ] Set up the admin account and trusted domains

```yaml
services:
  db:
    image: mariadb:11
    restart: unless-stopped
    environment:
      MARIADB_DATABASE: nextcloud
      MARIADB_USER: nextcloud
      MARIADB_PASSWORD: CHANGE_ME_DB
      MARIADB_ROOT_PASSWORD: CHANGE_ME_ROOT
    volumes: ["./db:/var/lib/mysql"]
    networks: [proxy]

  redis:
    image: redis:7-alpine
    restart: unless-stopped
    networks: [proxy]

  nextcloud:
    image: nextcloud:28
    restart: unless-stopped
    depends_on: [db, redis]
    environment:
      NEXTCLOUD_ADMIN_USER: admin
      NEXTCLOUD_ADMIN_PASSWORD: CHANGE_ME_ADMIN
      NEXTCLOUD_TRUSTED_DOMAINS: "nextcloud.example.com"
      MYSQL_HOST: db
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: CHANGE_ME_DB
      REDIS_HOST: redis
    volumes: ["./data:/var/www/html"]
    networks: [proxy]
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.nextcloud.rule=Host(`nextcloud.example.com`)"
      - "traefik.http.routers.nextcloud.entrypoints=websecure"
      - "traefik.http.routers.nextcloud.tls.certresolver=letsencrypt"
      - "traefik.http.services.nextcloud.loadbalancer.server.port=80"

networks:
  proxy:
    external: true
```

- [ ] Visit `https://nextcloud.example.com`, complete setup
- [ ] Create user groups and initial users

### Stage 2 — OnlyOffice (document collaboration)

- [ ] Deploy OnlyOffice DocumentServer in a separate container
- [ ] Link it to Nextcloud via the official app ("ONLYOFFICE" app in the Nextcloud app store)
- [ ] Configure the document server URL and JWT secret

```yaml
  onlyoffice:
    image: onlyoffice/documentserver:latest
    restart: unless-stopped
    environment:
      JWT_ENABLED: "true"
      JWT_SECRET: CHANGE_ME_DOCS_JWT
    networks: [proxy]
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.office.rule=Host(`office.example.com`)"
      - "traefik.http.routers.office.entrypoints=websecure"
      - "traefik.http.routers.office.tls.certresolver=letsencrypt"
      - "traefik.http.services.office.loadbalancer.server.port=80"
```

- [ ] In Nextcloud Settings РІвЂ вЂ™ OnlyOffice, set the server URL and secret
- [ ] Create a test .odt/.docx and open it in the browser; try simultaneous editing

**Note:** Collabora (CODE) is a lighter alternative if memory is tight. The integration works the same way via its own app.

### Stage 3 — Hardening and features

- [ ] Enable 2FA for admin accounts (Nextcloud supports TOTP)
- [ ] Set a proper file retention/versioning policy
- [ ] Configure external storage if you want to mount existing shares
- [ ] Decide whether to enable Nextcloud Talk or use the [Matrix guide](matrix-messenger.md) for chat

### Stage 4 — CRM: EspoCRM (lightweight option)

- [ ] Deploy EspoCRM container backed by MariaDB
- [ ] Publish behind Traefik at `crm.example.com`
- [ ] Configure outbound email (SMTP) — reuse the [Mail Server](mail-server.md) setup
- [ ] Create users, import contacts/leads

```yaml
  espocrm:
    image: espocrm/espocrm:latest
    restart: unless-stopped
    environment:
      ESPOCRM_DATABASE_HOST: db
      ESPOCRM_DATABASE_USER: espocrm
      ESPOCRM_DATABASE_PASSWORD: CHANGE_ME
      ESPOCRM_ADMIN_USERNAME: admin
      ESPOCRM_ADMIN_PASSWORD: CHANGE_ME
    volumes: ["./data:/var/www/html"]
    networks: [proxy]
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.crm.rule=Host(`crm.example.com`)"
      - "traefik.http.routers.crm.entrypoints=websecure"
      - "traefik.http.routers.crm.tls.certresolver=letsencrypt"
      - "traefik.http.services.crm.loadbalancer.server.port=80"
```

### Stage 4-alt — CRM: Odoo (full-suite option)

```yaml
  odoo:
    image: odoo:17
    restart: unless-stopped
    depends_on: [db]
    environment:
      HOST: db
      USER: odoo
      PASSWORD: CHANGE_ME
    volumes: ["./addons:/mnt/extra-addons", "./odoo-data:/var/lib/odoo"]
    networks: [proxy]
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.odoo.rule=Host(`odoo.example.com`)"
      - "traefik.http.routers.odoo.entrypoints=websecure"
      - "traefik.http.routers.odoo.tls.certresolver=letsencrypt"
      - "traefik.http.services.odoo.loadbalancer.server.port=8069"
```

Odoo needs its own PostgreSQL database (not the Nextcloud MariaDB).

### Stage 5 — Backup

- [ ] Add database dumps (Nextcloud DB, CRM DB) to the backup script
- [ ] Back up Nextcloud `data/` and CRM data volumes
- [ ] Wire into the [Backup with restic and Borg](backup-restic-borg.md) guide, including the document server

## Verification

- [ ] Nextcloud login works; file upload/download fine
- [ ] Two users can edit the same document simultaneously (OnlyOffice)
- [ ] Calendar/contacts sync with phone via CalDAV/CardDAV (Nextcloud auto-discovery)
- [ ] CRM login works; email integration delivers/sends
- [ ] After a backup restore, files and DB are intact

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| OnlyOffice shows "Cannot connect" | JWT secret mismatch or URL wrong | Check the app settings; verify `office.example.com` resolves and JWT matches |
| Nextcloud slow | No Redis or wrong DB indexes | Add Redis; run `occ maintenance:repair`; enable opcache |
| Large files timeout | PHP upload limits | Set `upload_max_filesize` and `post_max_size` (Nextcloud env) |
| CalDAV/CardDAV not syncing | Auto-discovery blocked | Ensure `nextcloud.example.com/.well-known` passes through Traefik |
| CRM emails not sent | SMTP not configured | Use the mail server guide SMTP settings with submission+auth |

## Related pages

- [Nextcloud Hub](../communications/hubs/nextcloud.md)
- [Odoo and ERPNext](../engineering/erp/index.md)
- [EspoCRM and SuiteCRM](../engineering/crm/index.md)
- [OnlyOffice and Collabora](../communications/hubs/onlyoffice.md)
- [Backup with restic and Borg](backup-restic-borg.md)
- [Mail Server guide](mail-server.md)