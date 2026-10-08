---
title: Backend Developer
parent: Learning Paths
---

# Learning Path: Backend Developer

A structured roadmap to become a Backend Developer. You build the server side of applications: APIs, data storage, business logic, authentication and integration. The role pairs one language mastered deeply with solid fundamentals of databases, HTTP/API design, and enough operations to ship and run your own code.

## 1. Role overview

Read the [Backend Developer role card](../roles/backend.md) first: what backend work covers and the typical boundaries with frontend, DBA and DevOps. Key idea: you write the code that stores and serves data reliably.

## 2. Foundations

- **One language, deeply**: pick [Python](../development/programming-languages/python.md) or [Go](../development/programming-languages/go.md); Java is an alternative in enterprise shops. Learn types, OOP/structs, error handling, async.
- **Algorithms and data structures**: big-O, lists, hashes, trees, sorting - enough to write efficient handlers.
- **Version control**: [Git](../development/version-control/git.md) - branches, merge, rebase, remotes.
- **Data modeling**: tables, relations, keys, indexes; when to use SQL versus NoSQL (key-value, document).
- **HTTP/API design**: methods, status codes, headers, REST and JSON; resources, authentication, idempotency.
- **Linux essentials**: [basics](../operating-systems/linux/index.md) - enough to deploy and debug.

**Milestone:** you can write a small REST service in your language, connect it to a database, and run it on a Linux server.

## 3. Core tools (by domain)

### Language and framework

- **Your chosen language** - [Python](../development/programming-languages/python.md) with Django/FastAPI, or [Go](../development/programming-languages/go.md) with its standard lib/gin.

### Databases

- [PostgreSQL](../databases/relational/postgresql.md) - the default relational database.
- [MariaDB / MySQL](../databases/relational/mariadb.md) - the other common relational engine.
- [Redis](../databases/nosql/redis.md) - in-memory cache and queues.

### API and messaging

- [Nginx](../communications/web/nginx.md) - reverse proxy in front of your API.
- **RabbitMQ / Kafka** - message brokers for async work (no dedicated page yet; study queue/stream concepts).

### Testing

- Unit and integration test frameworks for your language (pytest, go test, JUnit).
- End-to-end UI testing: **Selenium / Cypress / Playwright** ([Playwright page](../development/testing/playwright.md)) for API-driven features.

## 4. Practice

Do these hands-on, in order:

1. [Git Server with Gitea](../guides/git-server-gitea.md) - host your code and run basic CI.
2. [Docker Host with Traefik](../guides/docker-host-traefik.md) - deploy your own API in a container behind a reverse proxy.
3. [Recipes](../guides/recipes/index.md) - [SSH key auth](../guides/recipes/ssh-key-auth.md), [firewall rule](../guides/recipes/firewall-rule.md): deploy safely.
4. Build and ship a real REST API: CRUD, auth, DB-backed, tested, and live on a server.

## 5. Typical vacancy stack

The recurring stack in backend postings:

1. **Python + Django/FastAPI, or Java + Spring (or Go/Node)** - the core language/framework.
2. **PostgreSQL** - the primary database.
3. **Redis** - caching and queues.
4. **Docker** - containers.
5. **Git** - version control.
6. **Nginx** - reverse proxy.

**You are job-ready when:** you can design and implement a database-backed REST API from a spec, write tests, and deploy it behind a reverse proxy on a server - without searching for a tutorial on every endpoint.

## Related

- [Backend Developer role card](../roles/backend.md)
- [Frontend learning path](frontend.md) (full-stack pairing)
- [DBA role card](../roles/dba.md)
- [Guides](../guides/index.md)
- [Recipes](../guides/recipes/index.md)