---
title: "TypeScript Essentials"
tags: ["languages"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 TypeScript Essentials

Tags: #typescript #types
Difficulty: Medium
Status: Learning

## Definition

TypeScript adds static typing to JavaScript, helping developers catch errors earlier and communicate interfaces more clearly.

## Why it matters / when to use

TypeScript is common in React, Next.js, and modern frontend codebases. It makes APIs and data contracts more explicit and improves maintainability.

## How it works

TypeScript compiles to JavaScript while enforcing type checks. Common patterns include interfaces, unions, generics, utility types, and type narrowing.

## Code example

```ts
interface User {
  id: number;
  name: string;
  active?: boolean;
}

function printUser(user: User): void {
  console.log(`${user.name} (${user.id})`);
}

const user: User = { id: 42, name: "Asha" };
printUser(user);
```

## Time and space complexity

Type checking is compile-time, not runtime. The runtime cost is similar to equivalent JavaScript, but the static safety improves maintainability.

## Common mistakes and pitfalls

- Overusing `any`
- Confusing union types with JavaScript `||`
- Not understanding optional chaining and narrowing

## Interview questions

### Q: Why is TypeScript valuable in large codebases?
Model answer: It catches errors earlier, documents data contracts, and improves editor support and refactoring safety.

## Related topics

- [Java fundamentals](../java/java-fundamentals.md)
- [JavaScript essentials](../javascript/javascript-essentials.md)
- [React interview notes](../../03-frontend/react.md)
