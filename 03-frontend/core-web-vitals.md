---
title: "Core Web Vitals"
tags: ["frontend","performance"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Core Web Vitals

## Definition

Core Web Vitals are a set of metrics that reflect perceived loading speed, interactivity, and visual stability.

## Main metrics

- LCP: Largest Contentful Paint ? how fast the main content appears
- INP: Interaction to Next Paint ? responsiveness to user input
- CLS: Cumulative Layout Shift ? visual stability during load

## How to improve them

- Reduce JS bundle size and defer non-critical scripts.
- Use image optimization and lazy loading.
- Keep layout stable by reserving space for images and ads.
- Avoid expensive layout thrash and long blocking tasks.

## Interview answer pattern

> We optimize for the user experience where the cost is highest: first paint, interactivity, and layout stability. The right answer depends on the bottleneck, but the usual fixes are reducing blocking scripts, improving asset delivery, and removing layout churn.

## Related notes

- [Rendering and reconciliation](rendering-and-reconciliation.md)
- [Next.js rendering](nextjs-rendering.md)
- [Memoization and state](memoization-and-state.md)
