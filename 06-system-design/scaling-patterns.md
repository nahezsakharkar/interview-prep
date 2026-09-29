---
title: "Core Building Blocks"
tags: ["dsa"]
difficulty: hard
status: learning
last_reviewed: 2026-09-30
---

 Core Building Blocks

Tags: #system-design #scaling
Difficulty: Medium
Status: Learning

## Definition

The core building blocks of distributed systems include load balancers, caches, queues, databases, and service boundaries.

## Why it matters / when to use

Most interview-grade design questions are really about using these elements together to meet service-level goals.

## How it works

Each component addresses a specific bottleneck: caching reduces read latency, queues decouple work, and replication improves availability.

## Code example

```yaml
load_balancer:
  strategy: round_robin
cache:
  provider: redis
database:
  type: postgres
```

## Time and space complexity

Scaling features are evaluated by latency, throughput, failure modes, and cost rather than trivial Big O.

## Common mistakes and pitfalls

- Treating a database as a universal bottleneck fix
- Ignoring the cost of consistency and replication
- Forgetting single points of failure

## Interview questions

### Q: When should you use a queue?
Model answer: When you need to decouple producer and consumer throughput, smooth spikes, or run work asynchronously without impacting user-facing latency.

## Related topics

- [System design fundamentals](system-design-fundamentals.md)
- [API design patterns](api-design.md)
- [Case study: URL shortener](case-study-url-shortener.md)
