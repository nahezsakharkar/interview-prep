---
title: "CSS Fundamentals"
tags: ["frontend"]
difficulty: easy
status: revised
last_reviewed: 2026-09-30
---

 CSS Fundamentals

Tags: #css #frontend
Difficulty: Easy
Status: Revised

## Definition

CSS is used to control layout, typography, colors, responsiveness, and visual behavior across a web app.

## Why it matters / when to use

CSS determines how UI feels in real use. Good fundamentals help with alignment, spacing, responsiveness, and cross-browser behavior.

## How it works

Key concepts include the box model, layout modes like flexbox and grid, media queries, specificity, and cascade behavior.

## Code example

```css
.card {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 16px;
  padding: 1rem;
}
```

## Time and space complexity

CSS complexity is usually about rendering cost and specificity problems rather than algorithmic time complexity.

## Common mistakes and pitfalls

- Relying on absolute positioning for ordinary layout
- Ignoring specificity and cascade effects
- Not testing responsive breakpoints

## Interview questions

### Q: When would you prefer grid over flexbox?
Model answer: Use grid for multi-dimensional layout and precise alignment; use flexbox for one-dimensional arrangement along rows or columns.

## Related topics

- [Accessibility](accessibility.md)
- [Performance tuning](performance.md)
- [React interview notes](react.md)
