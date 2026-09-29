---
title: "Sharding and message queues"
tags: ["system-design","sharding","queues"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Sharding and message queues

## Sharding

Sharding splits data across multiple database instances so each node hosts a subset of the data.

### Common sharding keys

- user ID
- tenant ID
- region
- hash of a key

### Trade-offs

- Improves write scalability and storage distribution
- Adds complexity for joins, cross-shard transactions, and rebalancing
- Requires careful key selection to avoid hotspots

## Message queues

Queues separate producers from consumers and decouple latency-sensitive requests from expensive work.

### Typical use cases

- email / notification dispatch
- image processing
- retryable background jobs
- event fan-out

## Example

```text
API -> Queue -> Worker -> DB
```

## Interview guidance

- Use queues when burst traffic or slow downstream systems would otherwise impact user-facing latency.
- Use sharding when a single database becomes too large or too hot.

## Related notes

- [Load balancing and caching](load-balancing-and-caching.md)
- [Rate limiter](rate-limiter.md)
- [Notification system](notification-system.md)
