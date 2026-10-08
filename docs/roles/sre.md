---
title: Site Reliability Engineer (SRE)
parent: IT Roles
---

# Site Reliability Engineer (SRE)

SRE applies software engineering to operations: reliability is defined by measurable Service Level Objectives (SLOs) and error budgets, and the engineer owns detection, mitigation and prevention end to end. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Job duties

1. Define and maintain SLOs and error budgets for core services ([SLO and error budgets](#slo-and-error-budgets)).
2. Build observability: metrics, dashboards, logs, tracing ([Observability](#observability)).
3. Run incident response and postmortems end to end ([Incident response](#incident-response)).
4. Plan capacity and performance, including autoscaling and load testing ([Capacity and performance](#capacity-and-performance)).
5. Automate toil reduction and reliability engineering ([Automation and reliability engineering](#automation-and-reliability-engineering)).
6. Review architectures for failure tolerance and reliability ([Automation and reliability engineering](#automation-and-reliability-engineering)).
7. Write automation and tooling in Go, Python or Shell ([Languages](#languages)).

## Responsibility domains

### SLO and error budgets

- Service Level Objectives, Service Level Indicators and error-budget policy (concept and practice; see [standards reference](../foundations/standards/index.md)).
- Alerting on burn rate: [Alertmanager](../observability/alerting/alertmanager.md).
- Automated toil reduction driven by error-budget burn (concept), implemented via the tooling below.

### Observability

- Metrics: [Prometheus](../observability/monitoring/prometheus.md), [VictoriaMetrics](../observability/monitoring/victoriametrics.md).
- Dashboards: [Grafana](../observability/alerting/grafana.md).
- Logs: [Loki](../observability/logging/loki.md), [ELK/EFK](../observability/logging/elasticsearch.md), [Vector](../observability/logging/vector.md), [Fluentd](../observability/logging/fluentd.md).
- Tracing: [Jaeger](../observability/alerting/jaeger.md).
- Exporters: [Node Exporter](../observability/monitoring/node-exporter.md), [Process Exporter](../observability/monitoring/process-exporter.md).

### Incident response

- Alert routing and grouping: [Alertmanager](../observability/alerting/alertmanager.md), [Grafana on-call](../observability/alerting/grafana.md).
- Runbooks and postmortems stored as versioned documents (Git): [Git](../development/version-control/git.md).
- On-call scheduling tooling is usually commercial (PagerDuty, Opsgenie) or self-hosted (Keep), referenced as text.

### Capacity and performance

- Horizontal scaling of clusters: [Kubernetes](../orchestration/schedulers/kubernetes.md), [K3s](../orchestration/schedulers/k3s.md).
- Load testing: k6, Vegeta, Locust (referenced as text; not yet covered by a wiki page).
- Cluster autoscaling: Karpenter, Cluster Autoscaler (referenced as text).

### Automation and reliability engineering

- Infrastructure as Code: [Terraform](../automation/iac/terraform.md), [OpenTofu](../automation/iac/opentofu.md), [Pulumi](../automation/iac/pulumi.md).
- Configuration: [Ansible](../automation/configuration-management/ansible.md), [SaltStack](../automation/configuration-management/saltstack.md).
- GitOps to keep the system in the declared state: [Argo CD](../orchestration/gitops/argo-cd.md), [Flux](../orchestration/gitops/flux-cd.md).
- Chaos and reliability testing frameworks (Chaos Monkey, Litmus) referenced as text.

### Languages

- [Go](../development/programming-languages/go.md), [Python](../development/programming-languages/python.md), [Shell](../development/programming-languages/shell.md).

## Out of scope

- Business application feature development (developer).
- Routine desktop, user and hardware support (sysadmin).
- Primary ownership of the CI/CD delivery pipeline (DevOps - SRE consumes it).
- Building the internal developer platform products (Platform Engineer - overlapping).

## Career path

- **SRE → Platform Engineer** — when you move from guaranteeing services to building the shared infrastructure products everyone consumes.
- **SysAdmin → SRE** — the classic growth path for sysadmins who adopted automation and reliability metrics.
- **SRE ↔ DevOps** — many companies use the titles interchangeably; SRE leans on measurable reliability.

## Related

- [DevOps Engineer](devops.md)
- [Platform Engineer](platform-engineer.md)
- [System Administrator](sysadmin.md)