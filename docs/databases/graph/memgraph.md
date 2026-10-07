---
title: Memgraph
parent: Graph
---

# Memgraph

Memgraph is an open-source, in-memory graph database built for real-time analytics and high-throughput applications. It stores the graph in memory to deliver low-latency traversal and analytics, supports the Cypher query language, and provides enterprise features such as streaming ingestion and replication as part of its feature set.

## Key features

- In-memory storage for low-latency graph traversal
- Support for the Cypher query language
- Streaming ingestion from Kafka and other sources
- Replication and comprehensive procedures for graph analytics

## Notes for administrators

Because data is held in memory, size the cluster memory to the working data set and configure persistence and replication for durability.

## Resources

- [Official documentation](https://memgraph.com/docs)
- [Repository](https://github.com/memgraph/memgraph)