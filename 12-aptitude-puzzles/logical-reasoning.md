---
title: "Logical Reasoning"
tags: ["aptitude"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Logical Reasoning

Tags: #aptitude #logic
Difficulty: Medium
Status: Learning

## Definition

Logical reasoning tests how consistently you interpret statements, constraints, and relationships.

## Why it matters / when to use

It helps assess structured thinking under time pressure and with incomplete information.

## How it works

Start by listing conditions, eliminating impossible cases, and checking each conclusion against the original facts.

## Code example

```ts
const statements = [
  "All engineers are problem solvers.",
  "Asha is an engineer."
];

console.log(statements[0].includes("engineer") && statements[1].includes("engineer"));
```

## Time and space complexity

Not relevant.

## Common mistakes and pitfalls

- Making assumptions not explicitly supported
- Missing the difference between sufficient and necessary conditions
- Not testing multiple scenarios

## Interview questions

### Q: What is a good habit in logic tests?
Model answer: Write down the constraints, eliminate contradictions, and validate each conclusion before finalizing it.

## Related topics

- [Quant fundamentals](quant.md)
- [Classic puzzles](puzzles.md)
