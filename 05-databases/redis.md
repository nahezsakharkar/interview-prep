---
title: "Redis Interview Notes"
tags: ["database"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Redis Interview Notes

Tags: #database #redis
Difficulty: Medium
Status: Learning

## Definition

Redis is an in-memory data structure store used for caching, pub/sub, rate limiting, leaderboards, and session management.

## Why it matters / when to use

It is valuable when latency matters and data can be kept in memory or periodically persisted.

## How it works

Redis stores values as strings, hashes, sets, lists, sorted sets, and streams. TTLs and eviction policies help control memory.

## Code example

```bash
SET user:42 "Asha"
EXPIRE user:42 300
GET user:42
```

## Time and space complexity

Redis operations are typically O(1) or O(log n) for structured data structures, with memory cost proportional to the dataset size.

## Common mistakes and pitfalls

- Using Redis for long-lived primary data without backup strategy
- Forgetting to handle cache invalidation
- Overusing it for heavy transactional workloads

## Interview questions

### Q: Why is Redis good for rate limiting?
Model answer: Because it is fast, supports TTLs, and can maintain counters per key with low latency.

## Related topics

- [Caching strategies](../04-backend/caching.md)
- [Messaging systems](../04-backend/messaging.md)
- [Indexing and query optimization](indexing.md)
