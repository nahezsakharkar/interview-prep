---
title: "Normalization and Schema Design"
tags: ["database"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Normalization and Schema Design

Tags: #database #schema
Difficulty: Medium
Status: Learning

## Definition

Normalization organizes data to reduce redundancy and improve integrity by splitting related data into logical tables.

## Why it matters / when to use

Normalized schemas reduce anomalies and improve consistency but may require more joins.

## How it works

Normal forms such as 1NF, 2NF, and 3NF reduce duplicate data and enforce meaningful relationships between tables.

## Code example

```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  name VARCHAR(100)
);

CREATE TABLE orders (
  id INT PRIMARY KEY,
  user_id INT,
  total DECIMAL(10,2),
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

## Time and space complexity

Normalization mainly affects schema design and query complexity. More normalization usually means more joins and potential read overhead.

## Common mistakes and pitfalls

- Normalizing too aggressively without considering workload
- Duplicating facts across tables
- Missing foreign keys or unique constraints

## Interview questions

### Q: When do you denormalize?
Model answer: For read-heavy systems or analytics workloads, denormalization can reduce joins and improve query performance even at the cost of write complexity.

## Related topics

- [SQL essentials](sql-basics.md)
- [Transactions and isolation](transactions.md)
- [NoSQL patterns](nosql.md)
