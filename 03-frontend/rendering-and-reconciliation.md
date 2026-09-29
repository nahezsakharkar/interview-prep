---
title: "React rendering and reconciliation"
tags: ["frontend","react","rendering"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# React rendering and reconciliation

## Definition

React updates the UI by rendering components to a virtual tree and then reconciling the diff with the DOM to determine what actually changed.

## Why it matters

This is the core of React performance. Interviewers often ask why a component re-renders and how to keep render cost under control.

## How it works

- State/props changes trigger render evaluation.
- React creates a new virtual tree.
- Diffing compares old and new trees.
- Only the changed nodes are updated in the DOM.

## Key interview points

- `key` is important in lists because React uses it to match items across renders.
- Re-rendering can happen even when the DOM output is unchanged.
- Expensive compute should go behind memoization or be moved out of render.

## Example

```tsx
import React, { useState } from 'react';

export function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount((c) => c + 1)}>
      Count: {count}
    </button>
  );
}
```

## Common pitfalls

- Inline object or function props cause unnecessary re-renders.
- Missing `key` in list rendering produces unstable behavior.
- The render phase should stay pure and side-effect free.

## Related notes

- [Hooks and useEffect](hooks-and-useeffect.md)
- [Memoization and state](memoization-and-state.md)
- [Core Web Vitals](core-web-vitals.md)
