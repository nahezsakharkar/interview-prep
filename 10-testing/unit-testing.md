---
title: "Unit Testing"
tags: ["testing"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Unit Testing

Tags: #testing #unit
Difficulty: Medium
Status: Learning

## Definition

Unit tests verify isolated behavior of a small unit such as a function or class.

## Why it matters / when to use

They are fast, precise, and ideal for validating logic and edge cases.

## How it works

You set up a minimal input, execute a unit of behavior, and assert expected output or side effects.

## Code example

```ts
function add(a: number, b: number) {
  return a + b;
}

console.log(add(2, 3)); // 5
```

## Time and space complexity

The cost of a unit test is mostly execution time and maintainability, not algorithmic complexity.

## Common mistakes and pitfalls

- Testing implementation rather than behavior
- Over-mocking dependencies
- Failing to cover edge cases and boundary values

## Interview questions

### Q: What makes a good unit test?
Model answer: A good unit test is focused, deterministic, readable, and tied to external behavior rather than internal implementation choices.

## Related topics

- [Testing pyramid](test-pyramid.md)
- [Integration testing](integration-testing.md)
- [TDD workflow](tdd.md)
