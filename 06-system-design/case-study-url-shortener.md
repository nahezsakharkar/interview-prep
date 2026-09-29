---
title: "Case Study: URL Shortener"
tags: ["system-design"]
difficulty: hard
status: learning
last_reviewed: 2026-09-30
---

 Case Study: URL Shortener

Tags: #system-design #case-study
Difficulty: Hard
Status: Learning

## Definition

A URL shortener converts long URLs into compact codes and redirects clients while handling high throughput and availability.

## Why it matters / when to use

This is a classic system design interview problem because it blends API design, storage, caching, and scaling trade-offs.

## How it works

A short code is generated, stored with the original URL, and looked up efficiently. The system often uses a relational database or key-value store and a cache for hot links.

## Key design choices

- Use a hash or base62 encoded ID
- Cache popular links in Redis
- Use a short link table with unique keys
- Add rate limiting and analytics if needed

## Common pitfalls

- Assuming all cases are equally hot
- Ignoring collision handling
- Not considering redirect latency and DB load

## Interview questions

### Q: How would you handle high write and read traffic?
Model answer: Use a write-optimized data store for storing the mapping, cache hot links, and partition or shard by ID range if needed.

## Related topics

- [System design fundamentals](system-design-fundamentals.md)
- [Core building blocks](scaling-patterns.md)
- [API design patterns](api-design.md)
