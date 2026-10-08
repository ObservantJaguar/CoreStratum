---
title: Backend Developer
parent: IT Roles
---

# Backend Developer

The Backend Developer builds the server side of applications: business logic, data processing, APIs, integration with databases and external services. The role often specializes by language (Python, Java, Go, C#, PHP, Ruby...), but the responsibility domains stay the same.

## Job duties

1. Design and implement server-side business logic ([Server-side development](#server-side-development)).
2. Build and maintain APIs (REST, GraphQL, gRPC) ([APIs](#apis)).
3. Model, store and query data ([Databases and storage](#databases-and-storage)).
4. Integrate external services and message flows ([Integration and messaging](#integration-and-messaging)).
5. Ensure security, performance and reliability of endpoints ([Security and performance](#security-and-performance)).
6. Write automated tests for services ([Testing](#testing)).

## Responsibility domains

### Server-side development

- Languages (choose by team): [Python](../development/programming-languages/python.md), [Java](../development/programming-languages/index.md), [Go](../development/programming-languages/go.md), [C#](../development/programming-languages/index.md), PHP, Ruby.
- Frameworks: Django/FastAPI, Spring Boot, ASP.NET Core, Laravel, Rails (open source).

### APIs

- REST, GraphQL, gRPC; [HTTP](../foundations/protocols/index.md), [TLS](../foundations/standards/index.md).
- API gateways: [Traefik](../networking/load-balancing/traefik.md), [Nginx](../communications/web/nginx.md), [Envoy](../networking/load-balancing/envoy.md).

### Databases and storage

- Relational: [PostgreSQL](../databases/relational/postgresql.md), [MySQL/MariaDB](../databases/relational/mariadb.md).
- NoSQL/cache: [Redis](../databases/nosql/redis.md), [MongoDB](../databases/nosql/mongodb.md).
- Search: [Elasticsearch](../observability/logging/elasticsearch.md).

### Integration and messaging

- [RabbitMQ](../message-brokers/rabbitmq.md), [Kafka](../message-brokers/kafka.md).

### Security and performance

- [LUKS and cryptography concepts](../security/cryptography/index.md), OWASP basics, caching, profiling.

### Testing

- [Selenium](../development/testing/selenium.md), [Cypress](../development/testing/cypress.md), unit-level with pytest/JUnit.

## Out of scope

- UI/browser work (frontend).
- Infrastructure and deployment pipelines (DevOps) - though backend devs use them.
- Deep database administration (DBA).

## Career path

- **Backend → Senior Backend** — system design, scale, mentoring.
- **Backend → Fullstack** — add frontend skills.
- **Backend → DevOps/Platform** — infrastructure-oriented backend.

## Related

- [Frontend Developer](frontend.md)
- [Fullstack Developer](fullstack.md)
- [Software Engineer](software-engineer.md)
- [DBA](dba.md)