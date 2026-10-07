---
title: Platform Engineer
parent: IT Roles
---

# Platform Engineer

The Platform Engineer builds the shared internal platform that developers (and other engineering teams) consume: a thin, standardized layer of Kubernetes clusters, golden paths, CI runners and self-service tools. Where DevOps ships applications and SRE guarantees them, the Platform Engineer owns the reusable substrate. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Responsibility domains

### Internal developer platform

- Golden paths and developer self-service: Backstage (referenced as text).
- API and portal for provisioning requests (referenced as text).
- Shared service catalog and docs: [MkDocs](../development/documentation/mkdocs.md).

### Cluster and infrastructure foundation

- Cluster provisioning and management: [Kubernetes](../orchestration/schedulers/kubernetes.md), [K3s](../orchestration/schedulers/k3s.md).
- Infrastructure as Code backing the platform: [Terraform](../automation/iac/terraform.md), [OpenTofu](../automation/iac/opentofu.md).
- Cluster IDP and multi-tenancy: [Helm](../orchestration/package-management/helm.md), [Kustomize](../orchestration/package-management/kustomize.md).

### GitOps and delivery

- Declarative application delivery: [Argo CD](../orchestration/gitops/argo-cd.md), [Flux](../orchestration/gitops/flux-cd.md).
- Secrets for the platform: [Vault](../automation/secrets-management/vault.md), [External Secrets](../automation/secrets-management/external-secrets.md), [Sealed Secrets](../automation/secrets-management/sealed-secrets.md).

### CI/CD runners and shared pipelines

- Self-hosted runners and templates (GitLab CI, GitHub Actions referenced as text).
- Version control as the source of truth: [Git](../development/version-control/git.md), [GitLab CE](../development/version-control/gitlab.md).

### Service mesh and connectivity

- East-west traffic and mTLS: [Istio](../orchestration/service-mesh/istio.md), [Linkerd](../orchestration/service-mesh/linkerd.md), [Cilium](../orchestration/service-mesh/cilium.md).
- Service discovery and config: [Consul](../automation/state-management/consul.md), [etcd](../automation/state-management/etcd.md).

### Platform observability

- Metrics and logs for platform components: [Prometheus](../observability/monitoring/prometheus.md), [Grafana](../observability/alerting/grafana.md), [Loki](../observability/logging/loki.md), [Jaeger](../observability/alerting/jaeger.md).

## Out of scope

- Business application code and feature pipelines per product (developer/DevOps).
- Guaranteeing individual service SLOs (SRE - overlapping).
- Desktop, hardware, user support (sysadmin).
- Security program ownership (SecOps).

## Career path

- **DevOps → Platform Engineer** — progress from shipping releases to building the reusable infrastructure layer.
- **SRE → Platform Engineer** — leverage reliability work into platform products.
- **Cloud Engineer → Platform Engineer** — from consuming cloud to building the internal cloud-like platform.

## Related

- [DevOps Engineer](devops.md)
- [SRE](sre.md)
- [Cloud Engineer](cloud-engineer.md)