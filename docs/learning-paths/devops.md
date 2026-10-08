---
title: DevOps Engineer
parent: Learning Paths
---

# Learning Path: DevOps Engineer

A structured roadmap to become a DevOps Engineer. DevOps is a culture plus a job: you own the delivery pipeline, infrastructure-as-code, containers and application observability. The stack varies between companies, so this path teaches the *core* that recurs everywhere, then points to what to learn per domain.

## 1. Role overview

Read the [DevOps Engineer role card](../roles/devops.md) first: what the job duties are, the responsibility domains, and what is out of scope. Key idea: DevOps is the bridge between developers and operations.

## 2. Foundations

Before touching any tool, understand how systems actually work:

- **Operating systems**: [Linux basics](../operating-systems/linux/index.md) - filesystem, processes, users, permissions, network config.
- **The shell**: [Bash scripting](../development/programming-languages/shell.md) - loops, pipes, variables, cron.
- **Version control**: [Git](../development/version-control/git.md) - branches, merge, rebase, remotes.
- **Networking fundamentals**: [TCP/IP, DNS, HTTP, TLS](../foundations/protocols/index.md).
- Optional but recommended: one general-purpose language - [Python](../development/programming-languages/python.md).

**Milestone:** you can administer a Linux server from the terminal, write a script that automates several commands, and use Git for your own code.

## 3. Core tools (by domain)

### Containers

- [Docker](../containers/container-engines/docker.md) - images, containers, volumes, Compose.
- [Podman](../containers/container-engines/podman.md) - daemonless alternative (same skills transfer).
- [Buildah](../containers/image-builders/buildah.md) - building images without a daemon.

### Orchestration

- [Kubernetes](../orchestration/schedulers/kubernetes.md) - pods, deployments, services, ingress.
- [Helm](../orchestration/package-management/helm.md) - packaging and deploying charts.
- [K3s](../orchestration/schedulers/k3s.md) - lightweight Kubernetes for learning and edge.

### Infrastructure as Code

- [Terraform](../automation/iac/terraform.md) - declarative provisioning (learn one cloud's basics with it: AWS, Azure or GCP).
- [Ansible](../automation/configuration-management/ansible.md) - configuration management without agents.
- [Vault / SOPS](../automation/secrets-management/vault.md) - secrets management.

### CI/CD

- [GitLab CE / GitHub Actions](../development/version-control/gitlab.md) - pipelines, jobs, artifacts.
- [Argo CD / Flux](../orchestration/gitops/argo-cd.md) - GitOps delivery.
- [Jenkins](../development/version-control/index.md) - enterprise classic.

### Observability

- [Prometheus](../observability/monitoring/prometheus.md) - metrics collection.
- [Grafana](../observability/alerting/grafana.md) - dashboards.
- [Loki](../observability/logging/loki.md) - log aggregation.
- [Jaeger](../observability/alerting/jaeger.md) - tracing (advanced).

## 4. Practice

Do these hands-on, in order:

1. [Docker Host with Traefik](../guides/docker-host-traefik.md) - deploy a containerized service behind a reverse proxy with TLS.
2. [Git Server with Gitea](../guides/git-server-gitea.md) - host your own Git and run CI.
3. [Monitoring and Logging](../guides/monitoring-logging.md) - Zabbix + Grafana + Loki (classic stack).
4. [Backup with restic and Borg](../guides/backup-restic-borg.md) - because every pipeline needs recovery.
5. Then the short [recipes](../guides/recipes/index.md) - firewall rules, SSH keys, LVM, cron, snapshots.

## 5. Typical vacancy stack (what employers actually ask)

Analysis of real postings shows these tools dominate DevOps vacancies:

1. **Kubernetes + Docker** - present in almost every posting.
2. **GitLab CI or GitHub Actions** - the pipeline engine.
3. **Terraform + Ansible** - the IaC pair.
4. **AWS or Azure or GCP** - at least one cloud, with its CLI.
5. **Prometheus + Grafana** - the observability default.
6. **Bash + Python (or Go)** - scripting for tooling.
7. **Helm, Argo CD, Vault** - the "modern" extras that push the salary up.

**You are job-ready when:** you can deploy a small application to a Kubernetes cluster, manage its config with Terraform/Ansible, set up a CI pipeline that tests and deploys it, and monitor the result in Grafana - without looking things up every step.

## Related

- [DevOps role card](../roles/devops.md)
- [SRE learning path](sre.md)
- [Guides](../guides/index.md)
- [Recipes](../guides/recipes/index.md)