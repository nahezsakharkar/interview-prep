---
title: "05 - Databases"
tags: ["overview"]
difficulty: easy
status: revised
last_reviewed: 2026-09-30
---

 05 - Databases

This section covers relational and non-relational database fundamentals and the common trade-offs that appear in interviews.

## Notes

- [SQL essentials](sql-basics.md) — joins, group by, filtering, subqueries, normalization basics
- [Indexing and query optimization](indexing.md) — B-tree behavior, covering indexes, cardinality, EXPLAIN plans
- [Transactions and isolation](transactions.md) — ACID, locks, anomalies, isolation levels
- [Normalization and schema design](normalization.md) — 1NF to 3NF, denormalization trade-offs
- [NoSQL patterns](nosql.md) — document, key-value, columnar, and when to choose each
- [Redis interview notes](redis.md) — caching, pub/sub, TTL, persistence, rate limiting
- [Database Internals](internals.md) — B-Trees vs LSM, WAL, Buffer Pool, Storage Engines
- [MongoDB and Oracle Advanced](mongodb-oracle-advanced.md) — Aggregation pipelines and enterprise SQL

## Core interview questions

- When would you denormalize schema design?
- How does indexing improve or worsen write performance?
- What is a transaction isolation level and when should you choose it?
