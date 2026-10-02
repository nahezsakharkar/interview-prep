---
title: "Advanced Databases: MongoDB and Oracle"
tags: ["databases","mongodb","oracle"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Advanced Databases

## 1. MongoDB Deep Dive

MongoDB is a document-oriented NoSQL database.

### Aggregation Pipeline
The aggregation pipeline is a framework for data transformation. Stages are processed in sequence.
- **`$match`**: Filters documents (like `WHERE`).
- **`$group`**: Groups documents by a key and computes aggregates (like `GROUP BY`).
- **`$project`**: Reshapes the output documents.
- **`$lookup`**: Performs a left-outer join with another collection.
- **`$unwind`**: Deconstructs an array field into multiple documents.

### Indexing in MongoDB
- **Single Field Index**: Basic B-tree index.
- **Compound Index**: Index on multiple fields. **Order matters**: Equality fields first, then Sort fields, then Range fields (ESR rule).
- **Multikey Index**: Indexes arrays.
- **TTL Index**: Automatically removes documents after a certain time.

## 2. Oracle Database Specifics

Oracle is a heavy-duty relational database used in enterprise environments.

### Key Architectural Features
- **Tablespaces**: Logical storage units that group data files.
- **Undo/Redo Logs**: Ensure ACID properties. Undo handles rollbacks; Redo handles crash recovery.
- **Pl/SQL**: Procedural extension to SQL for creating stored procedures, triggers, and packages.

### Performance Tuning
- **Execution Plans**: Use `EXPLAIN PLAN` to see how Oracle retrieves data.
- **Hints**: Use `/*+ INDEX(table index) */` to force the optimizer to use a specific index.
- **Partitioning**: Splitting large tables into smaller, manageable pieces (Range, Hash, List partitioning).

## 3. SQL Window Functions

Window functions perform calculations across a set of table rows that are related to the current row.

### Common Functions
- `ROW_NUMBER()`: Assigns a unique number to each row.
- `RANK()` / `DENSE_RANK()`: Ranks rows (Dense doesn't skip numbers).
- `LEAD()` / `LAG()`: Access data from the next or previous row without a join.
- `SUM(...) OVER(...)`: Running totals.

### Example: Get the top 3 salaries per department
```sql
SELECT employee_name, salary, dept_id
FROM (
    SELECT *, 
    DENSE_RANK() OVER(PARTITION BY dept_id ORDER BY salary DESC) as rank
    FROM employees
) 
WHERE rank <= 3;
```

## Related notes

- [SQL basics](05-databases/sql-basics.md)
- [Indexing](05-databases/indexing.md)
- [Transactions](05-databases/transactions.md)
