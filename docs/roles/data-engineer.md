---
title: Data Engineer
parent: IT Roles
---

# Data Engineer

The Data Engineer builds and operates the data flows: extracting data from sources, transforming it, loading it into warehouses or analytical stores, and keeping the pipelines observable and correct. The role sits between the operational databases a DBA runs and the analysis a data analyst performs. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Responsibility domains

### Extraction and pipelines

- Batch and streaming orchestration: Apache Airflow, Apache Spark (referenced as text; see [workflow definition](../engineering/bi-gis/apache-superset.md) for the analytics side).
- Log/event shipping into processing: [Vector](../observability/logging/vector.md), [Fluentd](../observability/logging/fluentd.md).

### Transformation and processing (ETL/ELT)

- SQL transformations atop warehouses: [dbt](../engineering/bi-gis/index.md) as a discipline (referenced as text).
- Ingest and transform engines for analytical workloads (Spark, Flink referenced as text).

### Storage and warehouses

- Columnar analytical store: [ClickHouse](../databases/time-series/clickhouse.md).
- Relational warehouse/DWH: [PostgreSQL](../databases/relational/postgresql.md).
- Time-series source stores: [InfluxDB](../databases/time-series/influxdb.md).
- Object storage for raw/parquet data: [MinIO](../storage/distributed/minio.md), [Ceph (RGW/object)](../storage/distributed/ceph.md).

### Data catalogs and governance

- Column-level lineage and catalog tooling: DataHub, Amundsen (referenced as text).
- Documentation and catalog managed in version control: [MkDocs](../development/documentation/mkdocs.md), [Git](../development/version-control/git.md).

### Data quality and observability

- Validation and schema checks (dbt tests, Great Expectations referenced as text).
- Pipeline metrics and dashboards: [Grafana](../observability/alerting/grafana.md), [Prometheus](../observability/monitoring/prometheus.md).

## Out of scope

- Running end-user analytics dashboards and reports (BI analyst).
- Feature/business application code (developer).
- Operating the databases as a service (DBA - overlapping).
- Machine-learning model training (data scientist).

## Career path

- **DBA → Data Engineer** — broaden from operating stores to building data movement and modeling.
- **Data Engineer → Data Scientist** — when the focus shifts from pipelines to models and analysis.
- **Data Engineer → Platform Engineer** — when you build the shared data platform for the whole company.

## Related

- [Database Administrator (DBA)](dba.md)
- [Platform Engineer](platform-engineer.md)
- [DevOps Engineer](devops.md)