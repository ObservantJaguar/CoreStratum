---
parent: Practice
title: Guides
nav_order: 16
has_children: true
---

# Guides

Beyond the encyclopedia of individual tools, this section contains practical **roadmaps** for building complete, self-hosted solutions on open-source software. Each guide walks through a realistic scenario for a systems administrator or an SMB-sized organization that is choosing its own stack from scratch.

A guide is not a copy-paste manual for one tool. It is a **route map**: the goal, the architecture, the ordered stages with checklists, and how to verify the result. Where a tool already has a page in the encyclopedia, the guide links to it instead of repeating the description.

## Available guides

### Foundation layer

- [Docker Host with Traefik](docker-host-traefik.md) — the base layer: one server running containers behind a reverse proxy with automatic TLS.
- [Backup with restic and Borg](backup-restic-borg.md) — protecting all of the above with deduplicated, encrypted, offsite backups.

### Corporate services

- [Mail Server](mail-server.md) — Postfix, Dovecot, Rspamd and full SPF/DKIM/DMARC setup for a small domain.
- [Matrix Messenger](matrix-messenger.md) — self-hosted corporate messenger with voice and video calls (Synapse, Element, coturn).
- [XMPP Messenger](xmpp-messenger.md) — lightweight, fully decentralized messaging with audio and video (ejabberd, Jingle, coturn).
- [Nextcloud and CRM](nextcloud-crm.md) — corporate file cloud and document collaboration, plus a CRM you host yourself.
- [IP Telephony](ip-telephony.md) — PBX on open-source software (FreePBX / VitalPBX) with WebRTC softphones.

### DevOps layer

- [Monitoring and Logging](monitoring-logging.md) — Zabbix and Grafana for metrics, Loki for centralized logs.
- [Git Server with Gitea](git-server-gitea.md) — self-hosted Git hosting with CI basics.

## Guide template

Every guide follows the same structure so an administrator can quickly find the phases and decision points:

1. **Goal** — what you get at the end, in concrete terms.
2. **Scope and out of scope** — what the guide covers and what it deliberately does not.
3. **Prerequisites** — hardware, OS, domain names, preparation.
4. **Architecture** — diagram of the stack and its components.
5. **Roadmap** — ordered stages with checklists.
6. **Verification** — smoke tests to confirm the solution works.
7. **Troubleshooting** — the most common problems and their fixes.
8. **Related pages** — links into the encyclopedia.