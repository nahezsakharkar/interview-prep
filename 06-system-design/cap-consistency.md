---
title: "CAP theorem and consistency"
tags: ["system-design","consistency","cap"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# CAP theorem and consistency

## Definition

CAP says a distributed system can provide at most two of consistency, availability, and partition tolerance.

## Consistency models

- Strong consistency: reads see the latest committed data
- Eventual consistency: replicas converge over time
- Causal consistency: operations with dependencies are ordered
- Read-your-writes: a client can read the data it just wrote

## Trade-offs

- Strong consistency improves correctness, but increases latency and complexity.
- Eventual consistency makes some workloads easier to scale, but stale reads are possible.
- For payments, inventory, and account balance updates, strong consistency is usually required.

## Interview framing

> The right model depends on the business requirement. A shopping cart may tolerate eventual consistency; a payment ledger usually requires strong consistency and durable writes.

## Related notes

- [Scalability basics](scalability-basics.md)
- [Sharding and queues](sharding-and-queues.md)
- [Rate limiter](rate-limiter.md)
