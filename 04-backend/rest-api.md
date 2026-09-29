---
title: "REST API Design"
tags: ["backend"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 REST API Design

Tags: #backend #api
Difficulty: Medium
Status: Learning

## Definition

REST APIs expose resources through consistent HTTP semantics such as GET, POST, PUT, PATCH, and DELETE.

## Why it matters / when to use

REST remains a common standard for web services, internal APIs, and platform integrations. Good design makes systems predictable and easier to evolve.

## How it works

Resource-oriented routes, idempotency, status codes, pagination, and versioning help APIs remain stable and maintainable under load.

## Code example

```http
GET /users/42
Accept: application/json
```

## Time and space complexity

API design is not primarily about Big O; complexity is driven by system scaling, database access, and network latency.

## Common mistakes and pitfalls

- Using POST for everything instead of resource semantics
- Not handling pagination and filtering early enough
- Returning excessive payload sizes

## Interview questions

### Q: How do you version an API?
Model answer: Prefer versioning strategies that are explicit and stable, such as URI versioning or header-based negotiation, while keeping compatibility in mind.

## Related topics

- [Spring Boot essentials](spring-boot.md)
- [Authentication and authorization](auth.md)
- [Caching strategies](caching.md)
