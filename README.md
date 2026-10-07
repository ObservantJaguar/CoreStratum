# CoreStratum

**CoreStratum** is an open-source encyclopedia of open technologies — a curated reference for system administrators, DevOps engineers and other IT professionals.

The wiki is organized into three sections: **Theory** (foundations and knowledge), **Tools** (the software encyclopedia), and **Practice** (step-by-step guides for building self-hosted solutions).

## Contents

### Theory

| # | Section | Description |
|---|---------|-------------|
| 1 | [Foundations](docs/foundations/index.md) | Protocols, standards, licensing, history, people |

### Tools — the software encyclopedia

| # | Domain | Description |
|---|--------|-------------|
| 1 | [Operating Systems](docs/operating-systems/index.md) | Linux, BSD, illumos, Windows Server, RTOS |
| 2 | [Virtualization and Compute](docs/virtualization/index.md) | Hypervisors, containers, cloud virtualization |
| 3 | [Containers and Runtimes](docs/containers/index.md) | Container engines, image builders |
| 4 | [Cluster Orchestration](docs/orchestration/index.md) | Kubernetes, schedulers, GitOps |
| 5 | [Networking](docs/networking/index.md) | Diagnostics, firewalls, VPN |
| 6 | [Security](docs/security/index.md) | WAF, identity, cryptography, hardening |
| 7 | [Storage](docs/storage/index.md) | Block, object, distributed, backup |
| 8 | [Filesystems](docs/filesystems/index.md) | Linux, Windows, network, distributed |
| 9 | [Databases](docs/databases/index.md) | Relational, NoSQL, time-series |
| 10 | [Development](docs/development/index.md) | Build systems, debugging, version control |
| 11 | [Communications](docs/communications/index.md) | Web, email, VoIP, messaging |
| 12 | [Observability](docs/observability/index.md) | Monitoring, logging, alerting |
| 13 | [Infrastructure Automation](docs/automation/index.md) | IaC, configuration management |
| 14 | [Engineering Systems](docs/engineering/index.md) | CAD, ERP, CRM, BI/GIS |

### Practice — guides

| Guide | Description |
|-------|-------------|
| [Docker Host with Traefik](docs/guides/docker-host-traefik.md) | The base layer: containers behind a reverse proxy with automatic TLS |
| [Backup with restic and Borg](docs/guides/backup-restic-borg.md) | Encrypted, deduplicated backups with restore verification |
| [Mail Server](docs/guides/mail-server.md) | Postfix, Dovecot, Rspamd, SPF/DKIM/DMARC |
| [Matrix Messenger](docs/guides/matrix-messenger.md) | Synapse + Element + coturn with voice/video calls |
| [XMPP Messenger](docs/guides/xmpp-messenger.md) | ejabberd + Jingle, lightweight fully decentralized chat |
| [Nextcloud and CRM](docs/guides/nextcloud-crm.md) | Corporate file cloud, docs and a self-hosted CRM |
| [IP Telephony](docs/guides/ip-telephony.md) | FreePBX / VitalPBX with WebRTC softphones |
| [Monitoring and Logging](docs/guides/monitoring-logging.md) | Zabbix + Grafana + Loki |
| [Git Server with Gitea](docs/guides/git-server-gitea.md) | Self-hosted Git hosting with CI basics |

## How to use

Browse the sidebar or start at the [table of contents](docs/index.md). Pick a domain that matches your task, open the category, then read the page for a specific tool.

## Hosting

The wiki is built with [Jekyll](https://jekyllrb.com) and the [Just the Docs](https://just-the-docs.com) theme, and is designed to be published on [GitHub Pages](https://pages.github.com).

To build locally (the site sources live in `docs/`):

```bash
bundle install
bundle exec jekyll serve --source docs --destination docs/_site --config docs/_config.yml,docs/_config_local.yml
```

Then open `http://localhost:4000/CoreStratum/` (or the address shown in the terminal).

## License

TBD