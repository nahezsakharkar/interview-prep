---
title: "React Interview Notes"
tags: ["frontend"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 React Interview Notes

Tags: #react #frontend
Difficulty: Medium
Status: Learning

## Definition

React is a UI library that builds components using declarative rendering and a virtualized render model.

## Why it matters / when to use

React is a dominant frontend tool for building reusable, modular interfaces and large-scale web apps.

## How it works

React updates the UI by comparing the new virtual tree to the previous one and reconciling the smallest needed changes. Hooks allow state and lifecycle behavior in function components.

## Code example

```tsx
import React, { useState, useMemo } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  const doubled = useMemo(() => count * 2, [count]);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}, Doubled: {doubled}
    </button>
  );
}
```

## Time and space complexity

React rendering complexity depends on component structure and state updates. In practice, optimization focuses on avoiding unnecessary renders and expensive recomputation.

## Common mistakes and pitfalls

- Using stale state closures without a functional update
- Overusing re-renders in large lists
- Forgetting keys in list rendering

## Interview questions

### Q: Why do keys matter in React lists?
Model answer: Keys help React identify which items changed, were added, or removed, improving reconciliation correctness and performance.

## Related topics

- [Next.js interview notes](nextjs.md)
- [Browser internals](browser-internals.md)
- [Performance tuning](performance.md)
