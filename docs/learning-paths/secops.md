---
title: SecOps / Security Engineer
parent: Learning Paths
---

# Learning Path: SecOps / Security Engineer

A structured roadmap to become a Security Engineer. SecOps keeps the environment safe: you detect, investigate and respond to security events, keep systems hardened, manage identities, and scan for vulnerabilities. The work spans monitoring, hardening, identity and a bit of forensics - so the path is broad and hands-on from day one.

## 1. Role overview

Read the [SecOps role card](../roles/secops.md) first. Security engineering touches every layer of infrastructure, so awareness of the broader [infosec role](../roles/infosec.md) matters too. Key idea: you do not just build things - you assume they will be attacked and design for that.

## 2. Foundations

- **Linux administration**: [installation, filesystem, users, permissions, services](../operating-systems/linux/index.md).
- **Networking fundamentals**: [TCP/IP, TLS, DNS, HTTP](../foundations/protocols/index.md), ports, sockets.
- **Cryptography basics**: [hashing, signatures, TLS, key exchange](../security/cryptography/index.md).
- **Attack mindset**: how common attacks work - scanning, brute force, SQLi, XSS, privilege escalation - so you can spot and diagnose them.

**Milestone:** you can lock down a Linux host, reason about what an attacker's traffic looks like, and explain the crypto primitive behind TLS.

## 3. Core tools (by domain)

### Monitoring and detection

- [Wazuh](../security/monitoring/wazuh.md) - host-based security monitoring and HIDS.
- **Suricata** - signature-based network intrusion detection and prevention (no dedicated page yet; study IDS/IPS concepts).
- [CrowdSec](../networking/intrusion-prevention/crowdsec.md) - IP reputation and automated blocking.

### Vulnerability management

- [Trivy](../security/monitoring/trivy.md) - container and filesystem vulnerability scanning.
- [OpenVAS](../security/pentest/openvas.md) - network vulnerability scanner.
- [Nmap](../security/pentest/nmap.md) - port scanning and inventory.

### Identity and access

- [Keycloak](../security/authentication/keycloak.md) - SSO, OIDC, SAML.
- [FreeIPA](../security/directory-services/freeipa.md) - authentication and directory/domain services.

### Hardening

- [Lynis](../security/hardening/lynis.md) - hardening audit and compliance checks.
- [SELinux](../security/hardening/selinux.md) - mandatory access control on RHEL-family.
- [AppArmor](../security/hardening/apparmor.md) - application confinement on Debian/Ubuntu.

### Forensics basics

- [Sleuth Kit](../security/forensics/sleuth-kit.md) - disk and file-system analysis after an incident.

## 4. Practice

Do these hands-on, in order:

1. [Recipes](../guides/recipes/index.md) - [firewall rule](../guides/recipes/firewall-rule.md), [LUKS disk encryption](../guides/recipes/luks-setup.md), [SSH key auth](../guides/recipes/ssh-key-auth.md): the baseline hardening toolkit.
2. [Backup with restic and Borg](../guides/backup-restic-borg.md) - understand encrypted backups before you answer to one.
3. [Monitoring and Logging](../guides/monitoring-logging.md) - logs and metrics are the base all detection builds on.
4. Build a small lab: one vulnerable/stock server behind Suricata/Wazuh, scan it with Nmap + OpenVAS, and read the alerts.

## 5. Typical vacancy stack

The recurring tools in SecOps and security-engineer postings:

1. **Wazuh or ELK stack** - SIEM-style detection and log centralization.
2. **Trivy (or Grype/similar)** - vulnerability scanning.
3. **Nmap** - recon and inventory.
4. **Keycloak or FreeIPA** - identity and single sign-on.
5. **Lynis** - hardening and compliance.
6. **CrowdSec / Fail2ban** - protection and IP reputation.

**You are job-ready when:** you can harden a fresh Linux host, wire up centralized monitoring and detection, interpret a scan and an alert, respond to a basic incident, and manage identities with an identity provider - without reading how-to guides at every step.

## Related

- [SecOps role card](../roles/secops.md)
- [Infosec role card](../roles/infosec.md)
- [DevSecOps role card](../roles/devsecops.md) (recommended next - security in the pipeline)
- [Guides](../guides/index.md)
- [Recipes](../guides/recipes/index.md)