---
title: "OOP and Design Basics"
tags: ["cs-fundamentals","oop","design"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# OOP and Design Basics

## Definition

Object-Oriented Programming (OOP) is a paradigm based on the concept of "objects," which can contain data (attributes) and code (methods). It aims to increase modularity and reuse through abstraction.

## The Four Pillars of OOP

### 1. Encapsulation
Grouping data and the methods that operate on that data into a single unit (class) and restricting direct access to some of the object's components.
- **Mechanism**: Access modifiers (`private`, `protected`, `public`).
- **Value**: Prevents external code from putting an object in an invalid state.

### 2. Abstraction
Hiding complex implementation details and showing only the necessary features of an object.
- **Mechanism**: Abstract classes and Interfaces.
- **Value**: Reduces complexity by allowing the developer to focus on *what* the object does rather than *how* it does it.

### 3. Inheritance
Allowing a new class (subclass) to acquire the properties and methods of an existing class (superclass).
- **Mechanism**: `extends` keyword.
- **Value**: Promotes code reuse.
- **Risk**: "Fragile Base Class" problem where changes in the superclass break subclasses.

### 4. Polymorphism
The ability of different classes to be treated as instances of the same superclass through a uniform interface.
- **Static Polymorphism**: Method Overloading (same method name, different parameters).
- **Dynamic Polymorphism**: Method Overriding (subclass provides a specific implementation of a superclass method).

## Composition vs Inheritance

A critical design decision in OOP is choosing between "Is-a" (Inheritance) and "Has-a" (Composition).

| Aspect | Inheritance (Is-a) | Composition (Has-a) |
| :--- | :--- | :--- |
| **Binding** | Static (Compile-time) | Dynamic (Runtime) |
| **Coupling** | Tight coupling | Loose coupling |
| **Flexibility** | Rigid hierarchy | Highly flexible |
| **Example** | `Dog extends Animal` | `Car has Engine` |

**Recommendation**: Favor composition over inheritance to avoid deep, rigid hierarchies that are hard to refactor.

## Design Principles (Quick Reference)

- **SOLID**:
    - **S**ingle Responsibility: A class should have one reason to change.
    - **O**pen/Closed: Open for extension, closed for modification.
    - **L**iskov Substitution: Subtypes must be substitutable for their base types.
    - **I**nterface Segregation: Clients shouldn't depend on methods they don't use.
    - **D**ependency Inversion: Depend on abstractions, not concretions.
- **DRY**: Don't Repeat Yourself.
- **KISS**: Keep It Simple, Stupid.

## Working Code Example: Polymorphism and Composition

This TypeScript example shows how to implement a payment system using an interface (Abstraction) and composition.

```ts
// Abstraction
interface PaymentProcessor {
  process(amount: number): void;
}

// Implementation 1
class StripeProcessor implements PaymentProcessor {
  process(amount: number) {
    console.log(`Processing $${amount} via Stripe...`);
  }
}

// Implementation 2
class PayPalProcessor implements PaymentProcessor {
  process(amount: number) {
    console.log(`Processing $${amount} via PayPal...`);
  }
}

// Composition: The Checkout system HAS-A processor
class CheckoutSystem {
  constructor(private processor: PaymentProcessor) {}

  completePurchase(amount: number) {
    this.processor.process(amount);
  }
}

// Usage: We can switch processors at runtime (Polymorphism)
const stripeCheckout = new CheckoutSystem(new StripeProcessor());
stripeCheckout.completePurchase(100);

const paypalCheckout = new CheckoutSystem(new PayPalProcessor());
paypalCheckout.completePurchase(200);
```

**Complexity**:
- **Time**: Method calls are $O(1)$.
- **Space**: $O(1)$ auxiliary space.

## Interview questions

### Q1: What is the difference between an Interface and an Abstract Class?
**Model answer**: An **Interface** is a contract; it defines *what* a class must do but provides no implementation. A class can implement multiple interfaces. An **Abstract Class** can provide partial implementation (default methods) and maintain state (fields). A class can only extend one abstract class.

### Q2: Explain the Liskov Substitution Principle (LSP) with an example.
**Model answer**: LSP states that a subclass should be usable wherever its superclass is expected without breaking the program. A classic violation is the "Square-Rectangle" problem: if `Square` extends `Rectangle` and overrides `setWidth` to also change `height`, any function expecting a `Rectangle` will be surprised when changing the width also changes the height.

### Q3: What is a "Diamond Problem" in multiple inheritance?
**Model answer**: It occurs when a class inherits from two classes that both inherit from a single superclass. If the two intermediate classes override the same method, the final class doesn't know which one to use. Java solves this by only allowing single inheritance for classes but multiple inheritance for interfaces.

### Q4: How does encapsulation protect a system?
**Model answer**: By making fields `private` and providing `public` getters/setters, we can validate data before it's changed. For example, a `setAge(int age)` method can throw an error if the age is negative, which is impossible if the field were public.

### Q5: When would you use an Abstract Class instead of an Interface?
**Model answer**: I use an abstract class when several closely related classes share a significant amount of common code (e.g., a `BaseService` that handles logging and error reporting). I use an interface when I want to define a behavior that could be implemented by completely unrelated classes (e.g., `Comparable`).

## Related notes

- [Operating systems](../13-cs-fundamentals/os.md)
- [Networking](../13-cs-fundamentals/networking.md)
- [Design Patterns](../07-design-patterns/README.md)
