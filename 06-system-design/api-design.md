---
title: "API Design Patterns"
tags: ["system-design"]
difficulty: hard
status: learning
last_reviewed: 2026-09-30
---

 API Design Patterns

Tags: #system-design #api
Difficulty: Medium
Status: Learning

## Definition

API design is the art of defining resource boundaries, actions, contracts, and failure semantics clearly.

## Why it matters / when to use

Good API design reduces ambiguity, improves compatibility, and makes services easier to evolve.

## How it works

Clear route naming, request/response structure, pagination, rate limiting, and error handling are all part of good design.

## Code example

```http
GET /v1/users?page=2&limit=20

200 OK
{
  "data": [{"id": 1, "name": "Asha"}],
  "page": 2,
  "next": "/v1/users?page=3&limit=20"
}
```

## Time and space complexity

API design is more about operational cost and clarity than raw algorithmic complexity.

## Common mistakes and pitfalls

- Non-resource-oriented endpoints
- Overly large responses
- Weak error semantics and unclear versioning

## Interview questions

### Q: What makes an API "good"?
Model answer: Good APIs are clear, stable, resilient, easy to document, and consistent in how they handle success, errors, and versioning.

## Related topics

- [System design fundamentals](system-design-fundamentals.md)
- [Core building blocks](scaling-patterns.md)
- [Case study: URL shortener](case-study-url-shortener.md)
