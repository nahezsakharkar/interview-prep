---
title: "Database Internals: Storage & Retrieval"
tags: ["databases", "internals", "sde-iii", "system-design"]
difficulty: hard
status: learning
last_reviewed: 2026-10-03
---

# Database Internals: Storage & Retrieval

## Definition
The storage engine is the component of a DBMS responsible for managing how data is stored on disk and retrieved into memory. It balances the trade-off between **Write Amplification**, **Read Amplification**, and **Space Amplification**.

## Storage Engines: B-Trees vs. LSM Trees

### B-Trees (Read-Optimized)
Used by: PostgreSQL, MySQL (InnoDB), Oracle.
- **Mechanism**: Maintains a sorted balanced tree of pages. Updates happen **in-place**.
- **Pros**: Extremely fast reads (logarithmic time), efficient range scans.
- **Cons**: Random I/O for writes; fragmented pages over time.

### LSM Trees (Write-Optimized)
Used by: Cassandra, RocksDB, LevelDB.
- **Mechanism**: 
  1. Writes go to an in-memory **MemTable**.
  2. Once full, flushed to disk as a sorted **SSTable** (Sequential I/O).
  3. Background **Compaction** merges SSTables to remove duplicates/tombstones.
- **Pros**: High write throughput (sequential writes).
- **Cons**: Read amplification (must check multiple SSTables); requires compaction.

| Feature | B-Tree | LSM Tree |
| :--- | :--- | :--- |
| Write Pattern | Random I/O | Sequential I/O |
| Read Performance | Fast / Consistent | Slower (requires Bloom Filters) |
| Update Strategy | In-place | Append-only (Versioned) |
| Primary Use Case | RDBMS / General Purpose | High-write / NoSQL |

## Durability & The WAL (Write-Ahead Log)
To ensure **Atomicity** and **Durability** (ACID), databases use a WAL.
1. **The Rule**: No data page is written to disk until the change is first recorded in the log.
2. **The Flow**: `Request` $\rightarrow$ `Append to WAL (Sequential)` $\rightarrow$ `Update Buffer Pool` $\rightarrow$ `Ack to User`.
3. **Recovery**: On crash, the DB replays the WAL from the last **Checkpoint** to restore the state of the Buffer Pool.

## Indexing Internals
- **Clustered Index**: The table *is* the index. Rows are physically stored in the order of the index key. (Only one per table).
- **Non-Clustered Index**: A separate structure containing the key and a pointer (RID or Primary Key) to the actual row.
- **Index-Only Scan**: If the query only requests columns present in the index, the DB skips the "bookmark lookup" to the main table entirely.

## Buffer Pool Management
The Buffer Pool is a region of memory that caches disk pages.
- **Eviction**: Uses **LRU (Least Recently Used)** or **Clock** algorithms to decide which page to remove when the pool is full.
- **Dirty Pages**: Pages modified in memory but not yet flushed to disk. A background writer process asynchronously flushes these to minimize the impact on user transactions.

## Interview Mindset
- **The Trade-off**: If an interviewer asks "How do we speed up writes?", the answer is almost always "Move from B-Trees to LSM Trees" or "Use a WAL/Commit Log".
- **The Cost**: Every index added speeds up reads but slows down writes (because the index must be updated synchronously).

## Interview Questions
### Q1: Explain read-amplification in LSM trees and how Bloom Filters mitigate it.
**Model Answer**: Read-amplification occurs because a key might exist in any of the SSTables. Without optimization, we'd check every table. **Bloom Filters** are probabilistic structures that can tell us "definitely not in this table" or "maybe in this table", allowing us to skip most SSTables.

### Q2: Why are B-Trees better for range queries than Hash indexes?
**Model Answer**: Hash indexes map keys to buckets randomly. B-Trees maintain keys in sorted order. A range query in a B-Tree finds the start key and then simply traverses the leaf nodes sequentially.

## Related topics
- [Indexing and query optimization](indexing.md)
- [Transactions and isolation](transactions.md)
