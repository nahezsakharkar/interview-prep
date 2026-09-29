---
title: "Load balancing and caching"
tags: ["system-design","load-balancing","caching"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Load balancing and caching

## Load balancing

Load balancers spread traffic across servers and can provide health checks, connection management, and failover.

### Common strategies

- Round robin
- Least connections
- IP hashing
- Weighted routing

## Caching

Caching reduces repeated fetches by storing hot data closer to the caller.

### Common cache patterns

- Cache-aside
- Read-through
- Write-through
- Write-behind

### Cache trade-offs

- Faster reads, but stale data risk
- Must handle invalidation and consistency carefully
- Large caches increase memory pressure and operational complexity

## Example

```text
Client -> Load Balancer -> App Server -> Redis Cache -> Database
```

## Interview guidance

- Put read-heavy data in cache where expiry and invalidation are controlled.
- Do not treat cache as the system of record for critical data.
- Use load balancers to avoid a single failed instance becoming a single point of failure.

## Related notes

- [Scalability basics](scalability-basics.md)
- [CAP theorem and consistency](cap-consistency.md)
- [Rate limiter](rate-limiter.md)
