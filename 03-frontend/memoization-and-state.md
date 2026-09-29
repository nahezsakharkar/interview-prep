---
title: "Memoization and state management"
tags: ["frontend","react","state"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Memoization and state management

## Definition

Memoization avoids recomputing expensive values when inputs have not changed. State management is the way data flows through the app without causing inconsistent or unnecessary updates.

## When to memoize

- Expensive derived calculations
- Data that is stable across component renders
- Components with large child trees and repeated renders

## Example

```tsx
import React, { useMemo, useState } from 'react';

function ProductList({ items }: { items: number[] }) {
  const [filter, setFilter] = useState('all');

  const filtered = useMemo(() => {
    if (filter === 'all') return items;
    return items.filter((item) => item > 10);
  }, [items, filter]);

  return <div>{filtered.length}</div>;
}
```

## State strategy guidance

- Keep state as close as possible to where it is used.
- Avoid storing derived values in state if they can be computed.
- Use local state for UI state, server state for remote data, and external stores for shared complex domains.

## Common mistakes

- Memoizing too aggressively and making the code harder to reason about.
- Creating a derived state that can drift from the source of truth.
- Using component state for data that really belongs to a server or a global store.

## Related notes

- [Rendering and reconciliation](rendering-and-reconciliation.md)
- [Next.js rendering](nextjs-rendering.md)
- [Core Web Vitals](core-web-vitals.md)
