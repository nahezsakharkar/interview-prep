---
title: "JavaScript Essentials"
tags: ["languages"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 JavaScript Essentials

Tags: #javascript #async
Difficulty: Medium
Status: Learning

## Definition

JavaScript is a dynamic, single-threaded language with event-driven execution and a rich set of runtime features such as closures, promises, and async/await.

## Why it matters / when to use

JavaScript is central to browser interactivity and many modern full-stack stacks. Interviewers often test closures, hoisting, async behavior, and prototype fundamentals.

## How it works

Understanding scope, execution context, event loop, microtasks, and prototype inheritance explains much of JavaScript behavior.

## Code example

```js
const fetchUser = async () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Asha"), 100);
  });
};

(async () => {
  const user = await fetchUser();
  console.log(`User: ${user}`);
})();
```

## Time and space complexity

JavaScript runtime behavior is usually discussed in terms of algorithmic complexity, not language-level typing, so the same Big O rules apply.

## Common mistakes and pitfalls

- Misunderstanding `this` binding
- Forgetting the event loop ordering with microtasks and macrotasks
- Believing `const` makes values immutable

## Interview questions

### Q: What is the difference between `==` and `===`?
Model answer: `==` does type coercion; `===` compares both type and value without coercion.

## Related topics

- [TypeScript essentials](../typescript/typescript-essentials.md)
- [Browser internals](../../03-frontend/browser-internals.md)
- [React interview notes](../../03-frontend/react.md)
