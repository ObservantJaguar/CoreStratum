---
title: Centralized Logging
parent: Observability and Monitoring
grand_parent: Tools
---

# Centralized Logging

Centralized logging covers the collection, aggregation, and storage of textual events across distributed systems. The category is organized around the primary open-source stacks — the classic Elasticsearch-based ELK pipeline, the cloud-oriented EFK stack built on Fluentd and Fluent Bit, the resource-efficient PLG stack based on Grafana Loki and Promtail, and the high-performance Vector data pipeline.

## ELK — Elasticsearch Stack

- [Elasticsearch](elasticsearch.md) — distributed search engine, the core of the ELK stack.
- [Logstash](logstash.md) — server-side component for dynamic data processing and transformation.
- [Filebeat](filebeat.md) — lightweight agent shipping text log files to Elasticsearch.
- [Metricbeat](metricbeat.md) — specialized agent shipping system and application metrics to Elasticsearch.

## EFK — Fluentd Stack

- [Fluentd](fluentd.md) — universal data aggregator, a de-facto standard for cloud environments.
- [Fluent Bit](fluent-bit.md) — ultra-light log collector optimized for containers.

## PLG — Grafana Loki Stack

- [Grafana Loki](loki.md) — log storage system that indexes only metadata.
- [Promtail](promtail.md) — agent for scraping logs and forwarding them to Loki.

## Pipelines

- [Vector](vector.md) — high-performance Rust-based tool for building data pipelines.

## All-in-one platforms

- [Graylog](graylog.md) — centralized log management with search, alerting and dashboards.