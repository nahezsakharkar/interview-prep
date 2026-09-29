---
title: "Prompt Engineering"
tags: ["agentic-ai"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Prompt Engineering

Tags: #ai #prompting
Difficulty: Medium
Status: Learning

## Definition

Prompt engineering is the practice of designing inputs that guide models toward better, more structured, and more reliable outputs.

## Why it matters / when to use

It changes the quality of model output without necessarily changing the model itself.

## How it works

A good prompt usually adds the task, relevant context, desired format, constraints, and examples when helpful.

## Code example

```ts
const prompt = `
You are an expert technical interviewer.
Summarize the key trade-offs of caching in 5 bullets.
Keep the answer concise and concrete.
`;

console.log(prompt);
```

## Time and space complexity

Prompting cost is mostly token-based, so longer prompts have higher latency and inference cost.

## Common mistakes and pitfalls

- Making prompts too vague
- Mixing multiple tasks in one instruction
- Forgetting to clarify output format or success criteria

## Interview questions

### Q: How do you reduce hallucinations in prompting?
Model answer: Ground the model with relevant source material, ask for a factual answer with a cited source or structured evidence, and constrain the output format.

## Related topics

- [LLM basics](llm-basics.md)
- [RAG](rag.md)
- [Evaluation and testing](evals.md)
