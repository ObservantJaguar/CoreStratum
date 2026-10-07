---
grand_parent: Practice
title: Monitoring and Logging
parent: Guides
---

# Monitoring and Logging

## Goal

A self-hosted observability stack for a small organization and its servers:

- **Zabbix** — agent-based monitoring: CPU, memory, disk, network, services, and alerting (email/Telegram).
- **Grafana** — dashboards over Zabbix and other sources (Prometheus, Loki).
- **Grafana Loki + Promtail** — centralized log collection, search and correlation with metrics.

DevOps-oriented teams can swap Zabbix for **Prometheus + VictoriaMetrics**; this guide covers the Zabbix-first path and notes the alternative.

## Scope and out of scope

**In scope:**
- Zabbix server + agents + templates for Linux/Windows
- Alerting: email (via the mail server guide) and Telegram
- Grafana datasources: Zabbix, Prometheus, Loki
- Loki + Promtail log pipeline
- Backup of Zabbix DB, Grafana dashboards, Loki data

**Out of scope:**
- Distributed tracing (see Jaeger)
- Full log SIEM (see Wazuh under Security)
- High-availability of the monitoring itself

## Choosing your metrics backend

| | Zabbix | Prometheus + VictoriaMetrics |
|---|---|---|
| Model | Agent + server (push) | Pull/exporters + TSDB |
| Host inventory, discovery | Excellent, built-in | Requires service discovery/relabel |
| Alerting | Rich, built-in | Alertmanager |
| Learning curve | Medium-low | Medium-high (for beginners) |
| Best for | Traditional infra, heterogeneous OS | Cloud-native, containers, apps |

For a mixed SMB fleet (Windows + Linux + network devices), **Zabbix** is the lowest-friction choice. For a container/DevOps environment, use Prometheus + VictoriaMetrics.

## Prerequisites

- A monitoring server (small VM, 2�“4 GB RAM)
- The [Docker Host with Traefik](docker-host-traefik.md) foundation layer (optional but recommended for Grafana/Loki)
- Targets to monitor: Linux servers, Windows servers, network devices (SNMP)
- Notification channels: SMTP (see [Mail Server](mail-server.md)) or a Telegram bot

## Architecture

```
   Targets (Linux/Windows/Switches)
        |  agents / SNMP
        v
   Zabbix Server ----------------> Zabbix DB (PostgreSQL)
        |  alerts
        v
   Grafana ------> +--------------------+     Loki ----> Promtail ---> logs from hosts
                    | Zabbix datasource  |
                    +--------------------+     v
                                             Prometheus (optional)
                                             Alertmanager (optional)
```

## Roadmap

### Stage 1 — Install the Zabbix server

On Debian/Ubuntu (adapt to your distro):

```bash
wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_latest+debian12_all.deb
sudo dpkg -i zabbix-release_latest+debian12_all.deb
sudo apt update
sudo apt install -y zabbix-server-pgsql zabbix-frontend-php zabbix-nginx-conf zabbix-sql-scripts postgresql
```

- [ ] Create the database and user
- [ ] Import the schema
- [ ] Configure `zabbix_server.conf` DB credentials
- [ ] Start `zabbix-server`, `zabbix-agent` (on the server itself) and PHP/nginx

### Stage 2 — Install agents on hosts

**Linux:**

```bash
sudo apt install -y zabbix-agent
# /etc/zabbix/zabbix_agentd.conf
# Server=<zabbix-server-ip>, ServerActive=<zabbix-server-ip>, Hostname=<host>
sudo systemctl enable --now zabbix-agent
```

**Windows:** download the Zabbix agent MSI and install with `SERVER=<ip>`.

- [ ] Add hosts in the Zabbix web UI under **Data collection �� ’ Hosts**
- [ ] Link the template (e.g. "Linux by Zabbix agent", "Windows by Zabbix agent")
- [ ] Verify green availability and metrics within ~1 minute

### Stage 3 — Network devices via SNMP

- [ ] Enable SNMP on switches/routers (SNMPv2c community or SNMPv3)
- [ ] Add the device, link the "SNMP agents" template
- [ ] Check interface and traffic items appear

### Stage 4 — Actions and notifications

- [ ] Create user media (email) and, optionally, a Telegram webhook integration
- [ ] Create **trigger actions** for high CPU/disk/net problems
- [ ] Set recovery actions
- [ ] Send a test problem (e.g. stop a service) and confirm the alert fires

### Stage 5 — Grafana

- [ ] Deploy Grafana as a container (behind Traefik from the foundation layer) or via OS package
- [ ] Add the **Zabbix datasource** plugin (`grafana/grafana-zabbix` datasource) — see https://grafana.com/grafana/plugins/alexanderzobnin-zabbix-datasource/
- [ ] Import a community Zabbix dashboard or build your own host dashboard
- [ ] Add a Prometheus datasource too (when used) and Loki as a log datasource

```yaml
  grafana:
    image: grafana/grafana:latest
    restart: unless-stopped
    volumes: ["./data:/var/lib/grafana"]
    networks: [proxy]
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.grafana.rule=Host(`grafana.example.com`)"
      - "traefik.http.routers.grafana.entrypoints=websecure"
      - "traefik.http.routers.grafana.tls.certresolver=letsencrypt"
      - "traefik.http.services.grafana.loadbalancer.server.port=3000"
```

### Stage 6 — Loki and Promtail (centralized logs)

- [ ] Deploy **Loki** (container, single binary + config)
- [ ] Deploy **Promtail** agents on each server to ship logs
- [ ] Add Loki as a datasource in Grafana
- [ ] Write a few log queries; correlate with metrics on a dashboard

Example Loki config (`loki-local-config.yaml`):

```yaml
auth_enabled: false
server:
  http_listen_port: 3100
schema_config:
  configs:
    - from: 2024-01-01
      store: tsdb
      object_store: filesystem
      schema: v13
      index:
        prefix: index_
        period: 24h
common:
  path_prefix: /loki
  storage:
    filesystem:
      chunks_directory: /loki/chunks
      rules_directory: /loki/rules
  replication_factor: 1
```

Promtail config (`promtail-config.yaml`):

```yaml
clients:
  - url: http://loki:3100/loki/api/v1/push

scrape_configs:
  - job_name: system
    static_configs:
      - targets: [localhost]
        labels:
          job: system
          __path__: /var/log/*.log
```

### Stage 7 — Alerts to Telegram (optional)

- [ ] Create a Telegram bot via BotFather, get the token and chat id
- [ ] In Zabbix, add a "Telegram" media type (webhook) and a user with it
- [ ] In Grafana, configure contact points for dashboard alerting

### Stage 8 — Backup

- [ ] Back up the Zabbix PostgreSQL database nightly
- [ ] Back up Grafana dashboards (export JSON or back up the volume)
- [ ] Include Loki chunks/compactor data in the [Backup guide](backup-restic-borg.md) pipeline

## Verification

- [ ] Zabbix web UI shows all monitored hosts green
- [ ] A low disk-space trigger raises an alert and the email/Telegram notification arrives
- [ ] Grafana dashboard shows CPU/mem/disk trends for a host
- [ ] A log query in Grafana/Loki returns recent lines from a server
- [ ] After restoring the Zabbix DB, the UI and history come back

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Host "Not monitored" | Agent not running or firewall | Check `zabbix_agentd` service and TCP port 10050 |
| No data for SNMP device | SNMP not enabled / wrong community | Verify `snmpwalk` from the Zabbix server first |
| Alerts not sent | No action or media type unconfigured | Create action + user media; test trigger manually |
| Grafana datasource error | Plugin not installed | Install `alexanderzobnin-zabbix-datasource`; configure URL + DB credentials |
| Loki has no data | Promtail not shipping / wrong path | Check Promtail logs and `loki_ready` metrics; validate config |

## Related pages

- [Zabbix](../observability/monitoring/zabbix.md)
- [Grafana](../observability/alerting/grafana.md)
- [Loki and Promtail](../observability/logging/loki.md)
- [Prometheus and VictoriaMetrics](../observability/monitoring/prometheus.md)
- [Alertmanager](../observability/alerting/alertmanager.md)
- [Wazuh (SIEM/HIDS)](../security/monitoring/wazuh.md)