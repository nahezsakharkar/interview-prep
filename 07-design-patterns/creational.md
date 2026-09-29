---
title: "Creational Patterns"
tags: ["design-patterns"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Creational Patterns

Tags: #design-patterns #oop
Difficulty: Medium
Status: Learning

## Definition

Creational patterns control object creation so systems can be decoupled from concrete classes and created in a consistent way.

## Why it matters / when to use

They are useful when object creation is complex, needs validation, or should remain flexible.

## How it works

Common patterns include Factory, Builder, Abstract Factory, and Singleton. They manage creation logic so client code remains simpler and more adaptable.

## Code example

```ts
class UserBuilder {
  private name = "";

  setName(name: string) {
    this.name = name;
    return this;
  }

  build() {
    return { name: this.name };
  }
}

const user = new UserBuilder().setName("Asha").build();
console.log(user);
```

## Time and space complexity

The cost is tied to object creation overhead and complexity of configuration rather than algorithmic time.

## Common mistakes and pitfalls

- Using Singleton blindly for shared state
- Building too much complexity into constructors
- Making the factory too generic without a clear abstraction

## Interview questions

### Q: When is Builder useful?
Model answer: When an object has many optional fields or complex assembly steps and you want to avoid a constructor with too many parameters.

## Related topics

- [SOLID principles](solid.md)
- [Structural patterns](structural.md)
- [Behavioral patterns](behavioral.md)
