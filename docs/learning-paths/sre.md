---
title: Site Reliability Engineer
parent: Learning Paths
---

# Learning Path: Site Reliability Engineer

A structured roadmap to become a Site Reliability Engineer. SRE sits between development and operations and applies software engineering to reliability: you design for failure, turn operations into code, and hold the line on service-level objectives. The role reuses many DevOps skills but is deeper on observability, Kubernetes and incident response.

## 1. Role overview

Read the [SRE role card](../roles/sre.md) first: the responsibility domains, the SLO contract, and the balance between feature velocity and reliability. Key idea: SRE is DevOps with an explicit "availability budget" the team must live within.

## 2. Foundations

Before touching any tool, understand how systems actually work:

- **Operating systems**: [Linux basics](../operating-systems/linux/index.md) - filesystem, processes, users, networking, systemd.
- **The shell**: [Bash scripting](../development/programming-languages/shell.md) - automation, log processing, cron.
- **Networking fundamentals**: [TCP/IP, DNS, HTTP, TLS](../foundations/protocols/index.md).
- **Distributed systems concepts**: consistency, availability, partitioning (CAP), idempotency, retries and backoff, queues.
- **Reliability terms**: what SLO, SLA and SLI mean and how an error budget is computed.

**Milestone:** you can quantify the availability of a small service, define its SLIs, and reason about what breaks in a distributed setup.

## 3. Core tools (by domain)

### Observability

- [Prometheus](../observability/monitoring/prometheus.md) - metrics collection and PromQL.
- [Grafana](../observability/alerting/grafana.md) - dashboards and alerting.
- [Loki](../observability/logging/loki.md) - log aggregation.
- Tracing: [Jaeger](../observability/alerting/jaeger.md) and OpenTelemetry - distributed traces across service boundaries (text standpoint: standardize instrumentation, propagate trace context).
- [Alertmanager](../observability/alerting/alertmanager.md) - route and deduplicate alerts.

### Orchestration

- [Kubernetes](../orchestration/schedulers/kubernetes.md) - deep: pods, deployments, services, ingress, HPA, Node affinity, taints.
- [K3s](../orchestration/schedulers/k3s.md) - lightweight cluster for learning.
- [Helm](../orchestration/package-management/helm.md) - packaging charts.

### Infrastructure as Code

- [Terraform](../automation/iac/terraform.md) - declarative provisioning.
- [Pulumi](../automation/iac/pulumi.md) - programmatic IaC alternative (mention).

### Incident response

- Alertmanager routing and escalation chains.
- Runbooks, postmortems and SLO dashboards.
- On-call tooling: [Grafana OnCall](../observability/alerting/grafana.md) as the scheduler/escalation layer (mention).

## 4. Practice

Do these hands-on, in order:

1. [Monitoring and Logging](../guides/monitoring-logging.md) - build a full metrics + logs + alerting stack.
2. [Docker Host with Traefik](../guides/docker-host-traefik.md) - deploy a service behind a reverse proxy with TLS and health checks.
3. [Backup with restic and Borg](../guides/backup-restic-borg.md) - verified recovery is half of reliability.
4. Then the short [recipes](../guides/recipes/index.md) - firewall rules, SSH keys, cron, LVM.

## 5. Typical vacancy stack

The recurring tools in SRE/site-reliability postings:

1. **Prometheus + Grafana + Loki + Alertmanager** - the observability core.
2. **Kubernetes** - the deployment platform, often with Helm.
3. **Terraform** - infrastructure as code.
4. **Go or Python** - tooling and operator logic.
5. **k6 or Vegeta** - load testing and capacity validation.
6. **CI/CD (GitLab or GitHub Actions)** - the deployment pipeline.

**You are job-ready when:** you can monitor a service in Prometheus/Grafana, define an SLO with an error budget, route alerts sensibly, survive a real incident with a postmortem, and scale a Kubernetes deployment to handle load - without looking things up every step.

## Related

- [SRE role card](../roles/sre.md)
- [DevOps learning path](devops.md)
- [SysAdmin learning path](sysadmin.md)
- [Guides](../guides/index.md)
- [Recipes](../guides/recipes/index.md)