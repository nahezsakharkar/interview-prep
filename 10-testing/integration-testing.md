---
title: "Integration Testing"
tags: ["testing"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Integration Testing

Tags: #testing #integration
Difficulty: Medium
Status: Learning

## Definition

Integration tests validate that multiple components work together when connected in a realistic environment.

## Why it matters / when to use

They catch contract mismatches, configuration issues, and cross-system failures that unit tests may miss.

## How it works

You exercise a real or near-real boundary between modules, such as a DB, queue, or API client integration.

## Code example

```ts
async function createUserApi() {
  return { status: 200, body: { id: 1 } };
}

console.log(await createUserApi());
```

## Time and space complexity

Integration testing cost is dominated by environment setup and external dependencies rather than Big O.

## Common mistakes and pitfalls

- Testing too much of the whole system in one case
- Making tests flaky due to shared state
- Not isolating dependencies enough to debug failures

## Interview questions

### Q: Why do integration tests matter even if unit tests pass?
Model answer: They validate the contracts between services and components, which often breaks in real workloads even when the isolated logic is correct.

## Related topics

- [Testing pyramid](test-pyramid.md)
- [E2E testing](e2e.md)
- [TDD workflow](tdd.md)
