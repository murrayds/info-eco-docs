---
title: Querying Data with DuckDB
---

### Prerequisites
To write scripts to run queries with DuckDB, you must use the correct packages.  Package management is handled with miniconda environments.  Refer to [Miniconda] for a tutorial.

### Info
Currently, queries are run directly on .parquet files rather than DuckDB native databases.  .parquet files take up less space, but may have worse performance in some advanced operations.  Refer to the link below for documentation on writing scripts.

[DuckDB Python]

[Miniconda]: /miniconda
[DuckDB Python]:https://duckdb.org/docs/current/clients/python/overview
