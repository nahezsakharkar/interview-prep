---
title: "Accessibility"
tags: ["frontend"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Accessibility

Tags: #a11y #frontend
Difficulty: Medium
Status: Learning

## Definition

Accessibility ensures that software can be used by people with different abilities, including keyboard, screen-reader, and cognitive accessibility needs.

## Why it matters / when to use

Accessible interfaces are not optional; they improve usability and are often required for compliance and inclusive product design.

## How it works

Use semantic HTML, meaningful labels, visible focus states, sufficient contrast, and support for keyboard interactions.

## Code example

```html
<label for="email">Email</label>
<input id="email" type="email" aria-describedby="email-help" />
<small id="email-help">We will never share your email.</small>
```

## Time and space complexity

Accessibility concerns are usually not about algorithmic complexity. They are about usability and DOM semantics.

## Common mistakes and pitfalls

- Using non-semantic elements for interactive controls
- Missing focus states
- Relying only on color to communicate meaning

## Interview questions

### Q: What is ARIA for?
Model answer: ARIA helps describe roles, states, and properties when native semantics are not enough, but it should not replace semantic HTML.

## Related topics

- [Browser internals](browser-internals.md)
- [CSS fundamentals](css.md)
- [React interview notes](react.md)
