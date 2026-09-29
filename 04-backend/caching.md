---
title: "Caching Strategies"
tags: ["markdown"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Caching Strategies

Tags: #backend #performance
Difficulty: Medium
Status: Learning

## Definition

Caching stores data closer to the user or application to reduce repeated computation or database access.

## Why it matters / when to use

It is one of the most effective ways to improve latency and reduce load on downstream systems.

## How it works

Common patterns include cache-aside, read-through, write-through, and write-behind. TTLs and invalidation are critical for correctness.

## Code example

```ts
const cache = new Map<string, { value: string; expiresAt: number }>();

function getCached(key: string): string | null {
  const item = cache.get(key);
  if (!item) return null;
  if (Date.now() > item.expiresAt) {
    cache.delete(key);
    return null;
  }
  return item.value;
}
```

## Time and space complexity

- Read: usually O(1) average with a hash map or in-memory cache
- Space: O(n) based on cache size

## Common mistakes and pitfalls

- Caching stale data without invalidation
- Cache stampede under hot keys
- Using cache as the system of record for critical data

## Interview questions

### Q: When do you invalidate a cache?
Model answer: After writes that change a value, during TTL expiry, or when a dependent object changes. The invalidation strategy should match the data freshness requirement.

## Related topics

- [REST API design](rest-api.md)
- [Messaging systems](messaging.md)
- [Redis interview notes](../05-databases/redis.md)
