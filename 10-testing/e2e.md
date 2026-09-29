---
title: "E2E Testing"
tags: ["testing"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 E2E Testing

Tags: #testing #e2e
Difficulty: Medium
Status: Learning

## Definition

End-to-end tests verify that a product works from the user perspective, covering the full flow across layers.

## Why it matters / when to use

They catch issues in real journeys, such as login, checkout, or navigation, that isolated tests may miss.

## How it works

You simulate the real user path and assert that the UI, logic, and backend work together coherently.

## Code example

```ts
console.log("Visit login page");
console.log("Enter credentials");
console.log("Verify dashboard is visible");
```

## Time and space complexity

E2E tests are typically slower and more expensive due to environment setup and full-stack validation.

## Common mistakes and pitfalls

- Making test steps too brittle
- Waiting on arbitrary timers instead of real conditions
- Relying on one giant happy-path test for everything

## Interview questions

### Q: When is E2E testing worth it?
Model answer: When the user journey is critical, cross-system behavior matters, or a bug would be expensive if missed by lower-level tests.

## Related topics

- [Testing pyramid](test-pyramid.md)
- [Integration testing](integration-testing.md)
- [TDD workflow](tdd.md)
