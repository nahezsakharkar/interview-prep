---
title: "Structural Patterns"
tags: ["design-patterns"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Structural Patterns

Tags: #design-patterns #oop
Difficulty: Medium
Status: Learning

## Definition

Structural patterns describe how objects and classes can be composed to form larger structures while keeping them flexible and manageable.

## Why it matters / when to use

They help reduce coupling, simplify interfaces, and create reusable relationships between components.

## How it works

Examples include Adapter, Decorator, Facade, and Composite. They solve problems related to wrapping, composition, and compatibility.

## Code example

```ts
class Circle {
  draw() { console.log("Drawing circle"); }
}

class DecoratedCircle {
  constructor(private circle: Circle) {}
  draw() {
    this.circle.draw();
    console.log("with border");
  }
}
```

## Time and space complexity

These patterns are typically constant or linear in their composition logic, but the value is in structure and maintainability rather than raw speed.

## Common mistakes and pitfalls

- Adding patterns before a simpler solution exists
- Overusing wrappers and making code harder to read
- Mixing responsibilities in adapters or facades

## Interview questions

### Q: What is the difference between Adapter and Facade?
Model answer: Adapter converts one interface to another, while Facade provides a simplified interface over a complex subsystem.

## Related topics

- [SOLID principles](solid.md)
- [Creational patterns](creational.md)
- [Behavioral patterns](behavioral.md)
