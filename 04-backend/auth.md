---
title: "Authentication and Authorization"
tags: ["backend"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Authentication and Authorization

Tags: #security #backend
Difficulty: Medium
Status: Learning

## Definition

Authentication verifies who a user is; authorization decides what they are allowed to do.

## Why it matters / when to use

This is foundational for secure APIs, user systems, and multi-tenant applications.

## How it works

Common patterns include sessions, JWTs, OAuth2, and role-based or attribute-based authorization.

## Code example

```ts
const token = "jwt-token";
const payload = JSON.parse(Buffer.from(token.split(".")[1], "base64").toString());
console.log(payload.sub);
```

## Time and space complexity

Authentication overhead is usually tied to cryptographic operations and network cost rather than simple Big O complexity.

## Common mistakes and pitfalls

- Accepting unsigned tokens or unvalidated claims
- Mixing authentication and authorization logic
- Storing secrets in client-side code

## Interview questions

### Q: What is the difference between authN and authZ?
Model answer: Authentication answers "who are you?" while authorization answers "what are you allowed to do?".

## Related topics

- [REST API design](rest-api.md)
- [Spring Boot essentials](spring-boot.md)
- [Microservices patterns](microservices.md)
