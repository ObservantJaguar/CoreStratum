---
title: Cloud Engineer
parent: IT Roles
---

# Cloud Engineer

The Cloud Engineer builds and operates infrastructure on cloud platforms — AWS, Azure, GCP or private clouds like OpenStack. The role combines infrastructure as code, cloud-native services and cost/resilience thinking, and often overlaps with DevOps and Platform roles depending on the company. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Responsibility domains

### IaaS provisioning

- Public clouds: [AWS](../virtualization/cloud-virtualization/aws.md), [Azure](../virtualization/cloud-virtualization/azure.md), [GCP](../virtualization/cloud-virtualization/gcp.md).
- Private cloud: [OpenStack](../virtualization/cloud-virtualization/openstack.md).
- Shared principles: [VPCs, EC2/VMs, S3/object storage, IAM](../foundations/standards/index.md).

### Infrastructure as Code

- Provisioning: [Terraform](../automation/iac/terraform.md), [OpenTofu](../automation/iac/opentofu.md), [Pulumi](../automation/iac/pulumi.md).
- Image building: [Packer](../automation/provisioning/packer.md), [Cloud-Init](../automation/iac/cloud-init.md).
- Configuration after boot: [Ansible](../automation/configuration-management/ansible.md).

### Cloud networking

- In-cloud routing and load balancing: [HAProxy](../communications/web/haproxy.md), [Keepalived/VIP](../networking/load-balancing/keepalived.md), [Envoy](../networking/load-balancing/envoy.md).
- Hybrid/on-prem bridging: [WireGuard](../networking/vpn/wireguard.md), [OpenVPN](../networking/vpn/openvpn.md).
- Managed DNS and CDN are cloud-native services (referenced as text).

### Container orchestration in the cloud

- Managed and self-managed clusters: [Kubernetes](../orchestration/schedulers/kubernetes.md), [K3s](../orchestration/schedulers/k3s.md).
- Cluster install/package: [Helm](../orchestration/package-management/helm.md), [Kustomize](../orchestration/package-management/kustomize.md).

### Cost and FinOps

- Right-sizing, reservations and budget alerts (process; commercial tooling referenced as text).
- Bring-your-own-license and reserved-instance optimization (referenced as text).

### Migration

- On-prem to cloud workload lift-and-shift and re-platform (process, not a single tool).

## Out of scope

- Writing business application code (developer).
- Deep on-prem physical network design (network engineer - cloud engineer works cloud-native).
- Application feature delivery pipeline exclusively (DevOps - overlapping).
- Formal security architecture per se (though cloud security is a large part of the job).

## Career path

- **SysAdmin → Cloud Engineer** — classic migration of on-prem admins into cloud.
- **Cloud Engineer ↔ DevOps** — hybrid roles are extremely common ("Cloud DevOps Engineer").
- **Cloud Engineer → Platform Engineer** — when you move from consuming cloud to building the internal platform atop it.

## Related

- [DevOps Engineer](devops.md)
- [Platform Engineer](platform-engineer.md)
- [Network Engineer](network-engineer.md)