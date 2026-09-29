---
title: "SOLID Principles"
tags: ["design-patterns"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 SOLID Principles

Tags: #design-patterns #architecture
Difficulty: Medium
Status: Learning

## Definition

SOLID is a set of five design principles for building maintainable, understandable software.

## Why it matters / when to use

Interviewers often use these principles to assess whether your design reasoning is disciplined and robust.

## How it works

- Single Responsibility: one reason to change
- Open/Closed: extend behavior without modifying code
- Liskov Substitution: child types must be substitutable for parent types
- Interface Segregation: avoid forcing clients to depend on unused methods
- Dependency Inversion: depend on abstractions, not concrete classes

## Code example

```ts
interface PaymentProcessor {
  process(amount: number): void;
}

class StripePayment implements PaymentProcessor {
  process(amount: number) {
    console.log(`Charging ${amount} via Stripe`);
  }
}
```

## Time and space complexity

Design principles are conceptual; their cost is primarily architectural and maintenance-related rather than algorithmic.

## Common mistakes and pitfalls

- Treating interface-heavy code as automatically better
- Violating LSP with a subclass that changes semantics
- Overengineering simple classes to satisfy every principle

## Interview questions

### Q: Why is the Single Responsibility Principle valuable?
Model answer: It keeps modules easier to reason about, test, and change, reducing the risk of unrelated logic being coupled together.

## Related topics

- [Creational patterns](creational.md)
- [Structural patterns](structural.md)
- [Behavioral patterns](behavioral.md)
