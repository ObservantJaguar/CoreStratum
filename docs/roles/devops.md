---
title: DevOps Engineer
parent: IT Roles
---

# DevOps Engineer

DevOps unifies development and operations: automate the delivery pipeline, shorten feedback loops, make releases predictable. As a job title it usually means the person who owns CI/CD, infrastructure-as-code, containers and application observability. Because the stack varies a lot between companies, this page maps the role into responsibility domains and the technologies that recur most often in real vacancies.

## Responsibility domains

### Containers and orchestration

- Engines: [Docker](../containers/container-engines/docker.md), [Podman](../containers/container-engines/podman.md), [containerd](../containers/container-engines/containerd.md).
- Orchestration: [Kubernetes](../orchestration/schedulers/kubernetes.md), [K3s](../orchestration/schedulers/k3s.md), [Docker Swarm](../orchestration/schedulers/docker-swarm.md).
- Package/install: [Helm](../orchestration/package-management/helm.md), [Kustomize](../orchestration/package-management/kustomize.md).
- Build: [Buildah](../containers/image-builders/buildah.md), [Packer](../automation/provisioning/packer.md).
- Runtime: [CRI-O](../containers/container-runtimes/cri-o.md), [runc](../containers/container-runtimes/runc.md).

### CI/CD

- GitLab CI, GitHub Actions, Jenkins, [Argo CD](../orchestration/gitops/argo-cd.md), [Flux](../orchestration/gitops/flux-cd.md).
- Version control: [Git](../development/version-control/git.md), [GitLab CE](../development/version-control/gitlab.md), [Gitea](../development/version-control/gitea.md).

### Infrastructure as Code

- Provision: [Terraform](../automation/iac/terraform.md), [OpenTofu](../automation/iac/opentofu.md), [Pulumi](../automation/iac/pulumi.md).
- Configure: [Ansible](../automation/configuration-management/ansible.md), [Chef](../automation/configuration-management/chef.md), [Puppet](../automation/configuration-management/puppet.md), [SaltStack](../automation/configuration-management/saltstack.md).
- Secrets: [Vault](../automation/secrets-management/vault.md), [SOPS](../automation/secrets-management/sops.md), [External Secrets](../automation/secrets-management/external-secrets.md).
- State: [etcd](../automation/state-management/etcd.md), [Consul](../automation/state-management/consul.md).

### Application observability

- Metrics: [Prometheus](../observability/monitoring/prometheus.md), [VictoriaMetrics](../observability/monitoring/victoriametrics.md).
- Dashboards: [Grafana](../observability/alerting/grafana.md).
- Logs: [Loki](../observability/logging/loki.md), [ELK/EFK](../observability/logging/elasticsearch.md), [Vector](../observability/logging/vector.md).
- Tracing: [Jaeger](../observability/alerting/jaeger.md).
- Alerting: [Alertmanager](../observability/alerting/alertmanager.md).

### Scripting and languages

- Bash, [Python](../development/programming-languages/python.md), [Go](../development/programming-languages/go.md), [Shell](../development/programming-languages/shell.md).

### Cloud platforms (often)

- [AWS, Azure, GCP](../virtualization/cloud-virtualization/index.md), [OpenStack](../virtualization/cloud-virtualization/openstack.md).

## Out of scope

- Business application features and code (developer).
- Desktops, hardware, user support (sysadmin).
- Formal reliability ownership with SLOs/error budgets (SRE - blurred).
- Security program ownership (SecOps).

## Career path

- **DevOps → SRE** — shift focus from delivery to measurable reliability.
- **DevOps → Platform Engineer** — build the internal platform and shared tooling.
- **DevOps → DevSecOps** — embed security scans and policy checks into the pipeline.

## Related

- [SRE](sre.md)
- [Platform Engineer](platform-engineer.md)
- [DevSecOps](devsecops.md)
- [System Administrator](sysadmin.md)