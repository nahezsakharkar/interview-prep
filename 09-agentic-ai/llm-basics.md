---
title: "LLM Basics"
tags: ["agentic-ai"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 LLM Basics

Tags: #ai #llm
Difficulty: Medium
Status: Learning

## Definition

Large language models generate text by learning statistical patterns from massive training data and then predicting likely sequences.

## Why it matters / when to use

LLMs power chat interfaces, summarization, rewriting, and agentic workflows, but they also have important failure modes.

## How it works

Prompt structure, context window, training data, sampling settings, and model architecture influence output quality and cost.

## Code example

```ts
const prompt = "Summarize the trade-offs of caching in a distributed system.";
console.log(prompt);
```

## Time and space complexity

LLM cost is usually dominated by token usage and inference latency rather than conventional algorithmic complexity.

## Common mistakes and pitfalls

- Assuming the model always knows the current fact
- Overloading prompts without structure
- Ignoring evaluation and guardrails

## Interview questions

### Q: What makes LLM outputs unpredictable?
Model answer: The model predicts tokens probabilistically, so small changes in prompt wording, sampling temperature, or context can change output substantially.

## Related topics

- [RAG](rag.md)
- [Tool use and agents](tool-use-and-agents.md)
- [Prompt engineering](prompt-engineering.md)
