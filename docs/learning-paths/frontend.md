---
title: Frontend Developer
parent: Learning Paths
---

# Learning Path: Frontend Developer

A structured roadmap to become a Frontend Developer. You build what users see and interact with: markup, styling, interactivity and the bridge to backend APIs. The path starts with the core web platform, then adds one framework deeply plus the tooling to build, test and ship a single-page application.

## 1. Role overview

Read the [Frontend Developer role card](../roles/frontend.md) first. Key idea: frontend work is not just "HTML pages" - it is state management, performance, accessibility and API integration in the browser.

## 2. Foundations

- **HTML/CSS/JavaScript** - the web platform; JavaScript deeply (closures, async, events, the event loop).
- **DOM and browser APIs**: selecting and manipulating the DOM, fetch, localStorage, rendering lifecycle.
- **HTTP**: methods, status codes, headers, CORS - how the browser talks to the API.
- **Version control**: [Git](../development/version-control/git.md).
- **Basic algorithms**: time complexity, arrays, maps, recursion - enough for UI logic.

**Milestone:** you can build a reactive interactive page with vanilla JavaScript, talk to a REST API, and handle its loading/error states.

## 3. Core tools (by domain)

### Framework

- **One framework, deeply**: React, Vue or Svelte - components, state, props, effects, routing.

### Language and typing

- **TypeScript** - static typing over JavaScript (there is no dedicated JS/TS wiki page yet; study the TS handbook).
- [Git](../development/version-control/git.md) for branching and collaboration.

### Build tooling

- **Vite or Webpack** - dev server, bundling, HMR, code splitting.

### Testing and quality

- [Playwright](../development/testing/playwright.md) - end-to-end browser tests.
- **Cypress** - alternative E2E test runner (mention).
- [SonarQube](../development/analysis/sonarqube.md) - static code quality and coverage.

## 4. Practice

Do these hands-on, in order:

1. [Git Server with Gitea](../guides/git-server-gitea.md) - host your code and run a pipeline.
2. [Docker Host with Traefik](../guides/docker-host-traefik.md) - deploy your frontend build behind a reverse proxy.
3. [Recipes](../guides/recipes/index.md) - [SSH key auth](../guides/recipes/ssh-key-auth.md), [firewall rule](../guides/recipes/firewall-rule.md): secure deployment basics.
4. Build and ship your own SPA: a component tree, state, routing, API integration, tests, and a live build.

## 5. Typical vacancy stack

The recurring stack in frontend postings:

1. **React (or Vue/Angular)** - the framework.
2. **TypeScript** - typed JavaScript.
3. **Vite (or Webpack)** - build tooling.
4. **REST or GraphQL** - API integration.
5. **Playwright (or Cypress)** - end-to-end testing.
6. **Git** - version control.

**You are job-ready when:** you can build and ship a complete single-page application - components, state, routing, API calls and E2E tests - that passes review without hunting through a tutorial for every pattern.

## Related

- [Frontend Developer role card](../roles/frontend.md)
- [Backend learning path](backend.md) (full-stack pairing)
- [Fullstack role card](../roles/fullstack.md)
- [Guides](../guides/index.md)
- [Recipes](../guides/recipes/index.md)