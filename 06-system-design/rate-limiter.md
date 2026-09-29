---
title: "Rate limiter"
tags: ["system-design","rate-limiting"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Rate limiter

## Definition

A rate limiter controls how many requests a client or tenant can make over a time window. It protects backend capacity and limits abuse.

## Common algorithms

- Token bucket
- Leaky bucket
- Fixed window
- Sliding window log

## Trade-offs

- Token bucket is popular for burst-friendly traffic shaping.
- Fixed window is simple but can allow spikes at window boundaries.
- Sliding window provides better fairness but is more expensive to compute.

## Typical interview answer

> For a public API, I would use a token bucket at the gateway or per-user level, with quota rules based on tenant and endpoint. The limiter should reject or slow down excess traffic before it hits expensive downstream services.

## Related notes

- [Load balancing and caching](load-balancing-and-caching.md)
- [CAP theorem and consistency](cap-consistency.md)
- [URL shortener](url-shortener.md)
