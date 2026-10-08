---
title: Database Administrator (DBA)
parent: IT Roles
---

# Database Administrator (DBA)

The Database Administrator owns the databases: installation, configuration, performance, backups, replication and user access. The role is distinct from a developer because its success is measured by availability, integrity and recoverability rather than by features. This page maps the role into its responsibility domains and the concrete technologies that belong to each one.

## Job duties

1. Install, configure and upgrade database engines ([Relational database engines](#relational-database-engines)).
2. Operate backup and recovery for all databases ([Backups and recovery](#backups-and-recovery)).
3. Set up and maintain replication and high availability ([Replication and high availability](#replication-and-high-availability)).
4. Tune query performance and monitor databases ([Performance and monitoring](#performance-and-monitoring)).
5. Manage schema migrations and data layout ([Storage and layout](#storage-and-layout)).
6. Administer users, roles and access rights ([Relational database engines](#relational-database-engines)).
7. Maintain cache and document stores alongside relational engines ([In-memory and NoSQL adjacents](#in-memory-and-nosql-adjacents)).

## Responsibility domains

### Relational database engines

- [PostgreSQL](../databases/relational/postgresql.md), [MySQL](../databases/relational/mysql.md), [MariaDB](../databases/relational/mariadb.md).
- Embedded/lightweight: [SQLite](../databases/embedded/sqlite.md).

### In-memory and NoSQL adjacents

- Cache/key-value: [Redis](../databases/nosql/redis.md).
- Document store: [MongoDB](../databases/nosql/mongodb.md).

### Backups and recovery

- Point-in-time and logical backups: pg_dump, mysqldump (referenced as text); PostgreSQL-specific continuous backup with [Barman](../storage/backup/barman.md).
- Generic push/pull backup transported offsite: [restic](../storage/backup/restic.md), [BorgBackup](../storage/backup/borgbackup.md), [Rclone](../storage/backup/rclone.md).
- File-system snapshot backups for stores placed on ZFS: [ZFS snapshots](../storage/backup/zfs-snapshots.md).

### Replication and high availability

- Streaming replication / failover: Patroni or repmgr (referenced as text).
- MySQL/MariaDB replication and Galera (referenced as text).

### Performance and monitoring

- Query analysis and metrics via [Prometheus](../observability/monitoring/prometheus.md) + DB exporters, dashboards in [Grafana](../observability/alerting/grafana.md).
- Slow-query and index tuning (referenced as text).

### Storage and layout

- Underlying storage: [LVM](../storage/block/lvm.md), [ZFS](../storage/raid/openzfs.md), [mdadm](../storage/raid/mdadm.md).
- Network/shared filesystems for clustered storage: [NFS](../storage/network-filesystems/nfs.md), [Ceph (block/RBD)](../storage/distributed/ceph.md).

## Out of scope

- Writing business application features and query code (developer).
- General server, OS and hardware administration (sysadmin).
- Network and firewall engineering (network engineer).
- Formal security architecture (SecOps).

## Career path

- **SysAdmin → DBA** — deepen the database slice of generalist administration.
- **DBA → Data Engineer** — move from operating stores to building pipelines and warehouses.
- **DBA → DevOps/Platform** — when the role broadens into running databases as a managed platform.

## Related

- [System Administrator](sysadmin.md)
- [Data Engineer](data-engineer.md)
- [Platform Engineer](platform-engineer.md)