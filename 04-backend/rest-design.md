---
title: "REST design"
tags: ["backend","rest","api"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# REST design

## Principles

- Resources over actions
- Use HTTP methods consistently
- Use status codes to describe outcomes
- Keep APIs versionable and idempotent where appropriate

## Good resource design

- `/users/:id`
- `/orders/:id/items`
- `/products?category=books&page=2`

## Common status codes

- 200 OK
- 201 Created
- 204 No Content
- 400 Bad Request
- 401 Unauthorized
- 404 Not Found
- 409 Conflict
- 500 Internal Server Error

## Content negotiation

Use `Accept` headers and return JSON consistently. Avoid mixing multiple response styles in the same endpoint.

## Interview guidance

- Prefer nouns for resources; verbs should be represented by HTTP method.
- Use pagination and filtering on collection endpoints.
- Keep response schemas explicit and stable.

## Related notes

- [Spring Boot internals](spring-boot-internals.md)
- [JWT and OAuth2](jwt-oauth2.md)
- [Transactions and N+1](transactions-and-n-plus-one.md)
