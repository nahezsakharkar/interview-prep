---
title: "OOP and Design Basics"
tags: ["cs-fundamentals"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 OOP and Design Basics

Tags: #cs #oop
Difficulty: Medium
Status: Learning

## Definition

Object-oriented programming models software as objects with state and behavior, encouraging structure and abstraction.

## Why it matters / when to use

OOP is useful for modeling domains, reducing duplication, and designing maintainable systems.

## How it works

Core ideas are encapsulation, inheritance, polymorphism, and abstraction. Good design often balances reuse with simplicity.

## Code example

```ts
class User {
  constructor(public name: string) {}

  greet() {
    console.log(`Hello, ${this.name}`);
  }
}

const user = new User("Asha");
user.greet();
```

## Time and space complexity

Conceptual design is more important than Big O here; maintainability and clarity are the primary goals.

## Common mistakes and pitfalls

- Overusing inheritance where composition is better
- Creating deep class hierarchies without a need
- Breaking encapsulation by exposing too much mutable state

## Interview questions

### Q: What is the value of encapsulation?
Model answer: It keeps object internals protected, reduces accidental coupling, and makes systems easier to evolve without breaking consumers.

## Related topics

- [Operating systems](os.md)
- [Networking](networking.md)
- [Computer architecture](architecture.md)
