---
title: SecOps / Security Engineer
parent: IT Roles
---

# SecOps / Security Engineer

SecOps (Security Operations) is the practice of protecting the environment and responding to threats as they are detected. A Security Engineer designs, implements and operates the security controls: monitoring and detection, vulnerability management, access control and incident handling. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Responsibility domains

### Monitoring and detection

- Host IDS/SIEM: [Wazuh](../security/monitoring/wazuh.md), OSSEC (referenced as text).
- Network IDS/IPS: Suricata, Zeek (referenced as text).
- Behavior-rule engine on firewall logs: [CrowdSec](../networking/intrusion-prevention/crowdsec.md), [Fail2ban](../networking/intrusion-prevention/fail2ban.md).
- Log aggregation for detection: [ELK](../observability/logging/elasticsearch.md), Graylog (referenced as text).
- Vulnerability scanner feeding detection pipelines: [Trivy](../security/monitoring/trivy.md).

### Vulnerability management

- Container and filesystem scanning: [Trivy](../security/monitoring/trivy.md).
- Network vulnerability assessment: [OpenVAS](../security/pentest/openvas.md).
- Discovery and enumeration: [Nmap](../security/pentest/nmap.md).
- Commercial scanners (Nessus, Qualys) and Grype referenced as text.

### Identity and access

- Identity provider / SSO: [Keycloak](../security/authentication/keycloak.md), [Authentik](../security/authentication/authentik.md).
- Directory services: [FreeIPA](../security/directory-services/freeipa.md), [LLDAP](../security/directory-services/lldap.md), [Samba AD DC](../security/directory-services/samba4.md).
- Least-privilege elevation: [sudo](../security/hardening/sudo.md), [doas](../security/hardening/doas.md).

### Hardening and baselines

- Audit and hardening checks: [Lynis](../security/hardening/lynis.md).
- MAC enforcement: [SELinux](../security/hardening/selinux.md), [AppArmor](../security/hardening/apparmor.md).
- Disk and filesystem encryption: [LUKS](../security/cryptography/luks.md), [GNU Privacy Guard](../security/cryptography/gnupg.md).
- Web application firewall: [ModSecurity](../security/waf/modsecurity.md).

### Incident handling

- Detection to response workflow and evidence preservation (process), supported by monitoring and forensics tooling.
- Log integrity and pivoting sources for postmortem analysis: [Wazuh](../security/monitoring/wazuh.md), Graylog (referenced as text).

## Out of scope

- Day-to-day server administration and user help (sysadmin).
- Building application features (developer).
- Writing the CI/CD pipeline (DevOps) - though SecOps reviews it.
- Formal legal and compliance ownership (that is GRC/CISO - overlapping).

## Career path

- **SysAdmin → SecOps** — the natural lateral move for sysadmins who enjoyed hardening and monitoring.
- **SecOps → InfoSec/IR** — specialization into incident response and digital forensics.
- **SecOps ↔ DevSecOps** — SecOps guards the whole environment; DevSecOps embeds security into the software pipeline.

## Related

- [DevSecOps](devsecops.md)
- [InfoSec / Incident Response](infosec.md)
- [System Administrator](sysadmin.md)