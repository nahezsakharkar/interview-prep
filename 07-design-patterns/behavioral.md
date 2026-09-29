---
title: "Behavioral Patterns"
tags: ["design-patterns"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Behavioral Patterns

Tags: #design-patterns #oop
Difficulty: Medium
Status: Learning

## Definition

Behavioral patterns focus on communication between objects and how responsibilities are assigned or delegated.

## Why it matters / when to use

They help manage workflows, notifications, and event-driven logic without tightly coupling classes.

## How it works

Examples include Observer, Strategy, Template Method, and Command. They structure behavior around change and delegation rather than state explosion.

## Code example

```ts
interface Strategy {
  execute(a: number, b: number): number;
}

class AddStrategy implements Strategy {
  execute(a: number, b: number) { return a + b; }
}

class Calculator {
  constructor(private strategy: Strategy) {}
  calculate(a: number, b: number) {
    return this.strategy.execute(a, b);
  }
}
```

## Time and space complexity

Usually close to O(1) for direct delegation. The real value is extensibility and reducible coupling.

## Common mistakes and pitfalls

- Using Observer where direct method calls are sufficient
- Overengineering for small systems
- Not separating policy from execution flow

## Interview questions

### Q: Why use Strategy instead of a large conditional?
Model answer: It makes the algorithm selection explicit, easier to extend, and easier to test without embedding business rules in a branching method.

## Related topics

- [SOLID principles](solid.md)
- [Creational patterns](creational.md)
- [Structural patterns](structural.md)
