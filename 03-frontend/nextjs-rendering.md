---
title: "Next.js rendering"
tags: ["frontend","nextjs","rendering"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Next.js rendering

## Core rendering modes

### SSR: Server-Side Rendering

- HTML is generated on each request.
- Good for fresh, user-specific content.
- Higher latency and server load than static generation.

### SSG: Static Site Generation

- HTML is generated at build time.
- Best for content that changes rarely.
- Great for SEO and fast first paint.

### ISR: Incremental Static Regeneration

- Static pages are revalidated after a time interval.
- Useful for content that is mostly static but needs periodic refresh.

### App Router

- File-based routing with nested layouts and server components by default.
- Better fits modern app architecture and streaming patterns.

## Example

```tsx
export async function getStaticProps() {
  return {
    props: { time: new Date().toISOString() },
    revalidate: 60,
  };
}
```

## Interview guidance

- Use SSR when data changes per request or user.
- Use SSG when content is stable and public.
- Use ISR when data is mostly static but must refresh periodically.
- Default to server components for data fetching to keep the client bundle smaller.

## Common pitfalls

- Hydration mismatches between server-rendered HTML and client render output.
- Overusing client components when server components would be sufficient.
- Forgetting cache and revalidation strategy.

## Related notes

- [Rendering and reconciliation](rendering-and-reconciliation.md)
- [Core Web Vitals](core-web-vitals.md)
- [Memoization and state](memoization-and-state.md)
