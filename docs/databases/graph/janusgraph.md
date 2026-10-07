---
title: JanusGraph
parent: Graph
---

# JanusGraph

JanusGraph is a scalable, distributed graph database optimized for storing and querying huge graphs spread across a multi-machine cluster. It separates the graph workload from storage and indexes by plugging into backends such as Apache Cassandra, HBase, and Google Bigtable, and uses the Apache TinkerPop property graph framework with Gremlin as its query language.

## Key features

- Distributed graph storage across horizontally scalable cluster backends
- Pluggable backends including Cassandra, HBase, and Bigtable
- Integration with the Apache TinkerPop and Gremlin ecosystems
- Full-text, geospatial, and range indexing via external index backends

## Notes for administrators

JanusGraph depends on external storage and index backends, so design the backend topology and capacity planning for the expected data size and query patterns.

## Resources

- [Official documentation](https://janusgraph.org)
- [Repository](https://github.com/JanusGraph/janusgraph)