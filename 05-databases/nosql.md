---
title: "NoSQL Patterns"
tags: ["database"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 NoSQL Patterns

Tags: #database #nosql
Difficulty: Medium
Status: Learning

## Definition

NoSQL databases are designed for flexibility, horizontal scale, and workloads that differ from traditional relational structures.

## Why it matters / when to use

They are common for unstructured or semi-structured data, large-scale event logs, user profiles, and high-write workloads.

## How it works

Common types include document stores, key-value stores, wide-column stores, and graph databases. Each fits different access patterns and consistency needs.

## Code example

```json
{
  "userId": 42,
  "name": "Asha",
  "roles": ["admin", "editor"],
  "preferences": {
    "theme": "dark"
  }
}
```

## Time and space complexity

Depends on the database and workload. The main trade-offs are consistency, availability, and scale characteristics.

## Common mistakes and pitfalls

- Choosing NoSQL without a clear workload reason
- Ignoring schema evolution and data validation
- Assuming eventual consistency is always acceptable

## Interview questions

### Q: When would you choose a document store?
Model answer: When the data model is hierarchical, the access pattern is mostly by document or nested structure, and flexibility matters more than strong relational modeling.

## Related topics

- [SQL essentials](sql-basics.md)
- [Redis interview notes](redis.md)
- [Normalization and schema design](normalization.md)
