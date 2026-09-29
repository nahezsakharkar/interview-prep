---
title: "Scalability basics"
tags: ["system-design","scalability"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Scalability basics

## Definition

A system is scalable when it can handle more load, more users, or more data without a proportional drop in performance or stability.

## Key metrics

- Throughput: requests per second
- Latency: p50, p95, p99
- Availability: uptime and recovery behavior
- Cost: compute, storage, and data transfer cost

## Scaling strategies

- Vertical scaling: more CPU/RAM on one machine
- Horizontal scaling: add more instances behind a load balancer
- Read scaling: cache and replicas
- Write scaling: partitioning, queueing, and async patterns

```mermaid
flowchart TD
	load[Growing workload] --> bottleneck{Where is the bottleneck?}
	bottleneck -->|CPU or memory per instance| vertical[Scale up instance]
	bottleneck -->|Stateless app capacity| horizontal[Add instances behind load balancer]
	bottleneck -->|Read-heavy data| reads[Cache and read replicas]
	bottleneck -->|Write or storage limit| writes[Partition data or process asynchronously]
	vertical --> measure[Measure latency, throughput, and cost]
	horizontal --> measure
	reads --> measure
	writes --> measure
```

## Common interview answer

> Start with single-instance design, then identify bottlenecks. Scale reads with caching and replicas, scale writes with sharding or async workers, and add observability before you optimize prematurely.

## Related notes

- [Load balancing and caching](load-balancing-and-caching.md)
- [CAP theorem and consistency](cap-consistency.md)
- [Sharding and queues](sharding-and-queues.md)
