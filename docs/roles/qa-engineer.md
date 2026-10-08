---
title: QA / Test Automation Engineer
parent: IT Roles
---

# QA / Test Automation Engineer

The QA / Test Automation Engineer verifies that software meets its requirements and does not regress, and automates as much of that verification as makes sense. The role spans manual exploration, automated unit to end-to-end tests, and performance/load testing. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Job duties

1. Write and maintain test plans and test cases ([Unit and integration testing](#unit-and-integration-testing)).
2. Build unit, integration and end-to-end tests ([Unit and integration testing](#unit-and-integration-testing), [End-to-end and browser automation](#end-to-end-and-browser-automation)).
3. Automate UI and API regression testing ([End-to-end and browser automation](#end-to-end-and-browser-automation)).
4. Run load and performance testing ([Load and performance testing](#load-and-performance-testing)).
5. Enforce code quality and static-analysis gates ([Code quality and static analysis](#code-quality-and-static-analysis)).
6. Integrate tests into CI and report results ([CI integration and reporting](#ci-integration-and-reporting)).
7. Provision isolated test environments ([Test environment provisioning](#test-environment-provisioning)).

## Responsibility domains

### Unit and integration testing

- Test frameworks: JUnit (Java), pytest (Python) (referenced as text).
- Test-driven development workflow and version control: [Git](../development/version-control/git.md).

### End-to-end and browser automation

- UI automation: [Selenium](../development/testing/selenium.md), [Cypress](../development/testing/cypress.md), [Playwright](../development/testing/playwright.md).
- API testing: Postman, REST Assured (referenced as text).

### Load and performance testing

- Load generation: k6, JMeter, Locust (referenced as text).
- Result dashboards tied to [Grafana](../observability/alerting/grafana.md) and [Prometheus](../observability/monitoring/prometheus.md).

### Code quality and static analysis

- Code analysis and coverage gates: [SonarQube](../development/analysis/sonarqube.md).
- Linting and formatting enforced in CI.

### CI integration and reporting

- Running tests in pipelines (GitLab CI, GitHub Actions referenced as text).
- Allure/ReportPortal reporting referenced as text.

### Test environment provisioning

- Isolated runtimes and virtualized hosts for test runs: [Vagrant](../automation/provisioning/vagrant.md), [VirtualBox](../virtualization/hosted/virtualbox.md), [Docker](../containers/container-engines/docker.md).

## Out of scope

- Writing production application features (developer).
- Designing and tuning the test infrastructure at scale (DevOps/Platform).
- Business analysis and requirements ownership (BA - though QA informs it).
- Security-specific testing beyond functional checks (SecOps/DevSecOps).

## Career path

- **QA Engineer → Test Automation Engineer → SDET** — shift from writing tests to building the test framework and tooling.
- **QA Engineer → DevOps/Platform** — when you own the CI and test-infra layer.
- **QA Engineer → Business Analyst/QA Lead** — move toward process and requirement ownership.

## Related

- [DevOps Engineer](devops.md)
- [Platform Engineer](platform-engineer.md)