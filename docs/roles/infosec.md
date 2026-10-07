---
title: InfoSec / Incident Response
parent: IT Roles
---

# InfoSec / Incident Response

InfoSec is the security program owner: it writes the policies, runs the audit evidence, and leads incident response end to end. Where SecOps operates the detection tooling, InfoSec decides what is protected, how to respond when something happens, and how to prove compliance. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Responsibility domains

### Policy and governance

- Security policy, standards and procedures maintained as versioned documents: [Git](../development/version-control/git.md).
- Risk treatment and control selection (process; frameworks such as ISO 27001 referenced as text).

### Monitoring and endpoint protection

- Host IDS/SIEM and endpoint telemetry: [Wazuh](../security/monitoring/wazuh.md), OSSEC (referenced as text).
- Log collection for SIEM: [ELK](../observability/logging/elasticsearch.md), [Vector](../observability/logging/vector.md), Graylog (referenced as text).

### Incident response

- Detection-to-remediation workflow and evidence preservation (process), supported by monitoring and forensics tooling.
- Remote protection during an active incident: [Fail2ban](../networking/intrusion-prevention/fail2ban.md), [CrowdSec](../networking/intrusion-prevention/crowdsec.md).

### Digital forensics

- Disk image acquisition and analysis: [Guymager](../security/forensics/guymager.md), [Foremost](../security/forensics/foremost.md), [The Sleuth Kit](../security/forensics/sleuth-kit.md).
- Memory forensics: [Volatility](../security/forensics/volatility.md).

### Audit and compliance evidence

- Configuration audit and hardening posture: [Lynis](../security/hardening/lynis.md).
- Cryptographic integrity of recorded evidence: [GNU Privacy Guard](../security/cryptography/gnupg.md), [LUKS](../security/cryptography/luks.md) for at-rest protection.
- Vulnerability posture summary: [OpenVAS](../security/pentest/openvas.md), [Trivy](../security/monitoring/trivy.md).

### Cryptography and secrets hygiene

- Key management and signing: [GNU Privacy Guard](../security/cryptography/gnupg.md).

## Out of scope

- Operating day-to-day security tooling and vulnerability fixing (SecOps - overlapping).
- Embedding scans into delivery pipelines (DevSecOps).
- Server and network administration (sysadmin/network engineer).
- Legal counsel and negotiation (lawyer/CISO level).

## Career path

- **SecOps → InfoSec/IR** — move from operating detection tooling to owning policy and incident command.
- **InfoSec → CISO / Security Architect** — senior path into program and strategy ownership.
- **InfoSec/IR → DevSecOps** — when focus shifts to embedding security into software delivery.

## Related

- [SecOps / Security Engineer](secops.md)
- [DevSecOps](devsecops.md)
- [System Administrator](sysadmin.md)