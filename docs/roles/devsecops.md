---
title: DevSecOps
parent: IT Roles
---

# DevSecOps

DevSecOps embeds security into the software delivery lifecycle instead of bolting it on at the end. The practitioner extends the DevOps pipeline with automated checks: scanning code, dependencies and container images for vulnerabilities, detecting secrets, and enforcing policy as code. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Responsibility domains

### SAST and DAST

- Static application security testing: SonarQube (self-hosted, see [SonarQube](../development/analysis/sonarqube.md)); Semgrep, CodeQL (referenced as text).
- Dynamic application security testing: OWASP ZAP, Burp Suite (referenced as text).

### Dependency and image scanning

- Container and filesystem vulnerability scanning: [Trivy](../security/monitoring/trivy.md).
- SBOM and supply-chain metadata: syft, Grype (referenced as text).
- Registry hygiene and image signing: cosign/Sigstore (referenced as text).

### Secrets management

- Central secrets engine: [Vault](../automation/secrets-management/vault.md), [OpenBao](../automation/secrets-management/openbao.md).
- Git-encrypted secrets: [SOPS](../automation/secrets-management/sops.md), [age](../automation/secrets-management/age.md).
- In-cluster reconciliation: [Sealed Secrets](../automation/secrets-management/sealed-secrets.md), [External Secrets](../automation/secrets-management/external-secrets.md).

### Policy as code

- OPA (Open Policy Agent) and Conftest (referenced as text) for policy checks over configs and IaC.
- Kubernetes admission policy: Kyverno (referenced as text).
- Infrastructure validation at apply time: [Terraform](../automation/iac/terraform.md), [OpenTofu](../automation/iac/opentofu.md) with policy gates.

### Secure supply chain and GitOps

- Controlled delivery of commit to production: [Argo CD](../orchestration/gitops/argo-cd.md), [Flux](../orchestration/gitops/flux-cd.md).
- Version control and merge-request review: [GitLab CE](../development/version-control/gitlab.md), [Gitea](../development/version-control/gitea.md), [Forgejo](../development/version-control/forgejo.md).
- Provenance and SLSA conformance (referenced as text).

## Out of scope

- Operating the whole enterprise security program (SecOps/CISO).
- Building application features (developer).
- Manual penetration testing engagements (pentester).
- Day-to-day infrastructure operations (sysadmin/DevOps).

## Career path

- **DevOps → DevSecOps** — DevOps engineers who add security automation to their pipelines grow into this.
- **DevSecOps ↔ SecOps** — DevSecOps guards the pipeline; SecOps guards the environment; they exchange findings constantly.
- **DevSecOps → Security Architect** — long-term senior path.

## Related

- [SecOps / Security Engineer](secops.md)
- [DevOps Engineer](devops.md)
- [InfoSec / Incident Response](infosec.md)