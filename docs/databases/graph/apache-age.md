---
title: Apache AGE
parent: Graph
---

# Apache AGE

Apache AGE (A Graph Extension) is a PostgreSQL extension that provides graph database capabilities directly on top of a PostgreSQL database. It adds graph modeling and querying through openCypher, allowing Graph data to be queried and managed alongside traditional relational data within the same database and tooling.

## Key features

- Graph functionality implemented as a PostgreSQL extension
- OpenCypher query language alongside standard SQL
- Graph data stored and managed in the same database as relational data
- Leverages existing PostgreSQL reliability, tooling, and administration

## Notes for administrators

Because Apache AGE runs inside PostgreSQL, no separate graph database needs to be operated; blending relational and graph workloads in one instance simplifies infrastructure but shares the same compute and storage resources.

## Resources

- [Official documentation](https://age.apache.org)
- [Repository](https://github.com/apache/age)