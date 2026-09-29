---
title: "SQL Essentials"
tags: ["database"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 SQL Essentials

Tags: #sql #database
Difficulty: Medium
Status: Learning

## Definition

SQL is the standard language for querying and managing relational databases.

## Why it matters / when to use

It is used for structured data, transactions, reporting, aggregations, and normalized data models.

## How it works

SQL supports tables, rows, indexes, joins, filters, grouping, and constraints. Core operations include SELECT, JOIN, WHERE, GROUP BY, and ORDER BY.

## Code example

```sql
SELECT user_id, COUNT(*) AS order_count
FROM orders
WHERE created_at >= '2025-01-01'
GROUP BY user_id
ORDER BY order_count DESC;
```

## Time and space complexity

Depends on the query plan, indexes, table size, and join strategy. In practice, index design and query structure matter more than abstract Big O alone.

## Common mistakes and pitfalls

- Forgetting to filter before grouping
- Using `SELECT *` without clear need
- Not understanding join semantics

## Interview questions

### Q: What is the difference between `INNER JOIN` and `LEFT JOIN`?
Model answer: `INNER JOIN` returns only matching rows, while `LEFT JOIN` preserves all rows from the left table and fills missing matches with `NULL`.

## Related topics

- [Indexing and query optimization](indexing.md)
- [Transactions and isolation](transactions.md)
- [Normalization and schema design](normalization.md)
