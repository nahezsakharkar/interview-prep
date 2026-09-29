---
title: "Evaluation"
tags: ["agentic-ai","evaluation"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Evaluation

## Definition

Evaluation tells you whether an agent or model is actually improving in the scenarios that matter.

## What to measure

- correctness and grounding
- latency and cost
- tool-call success rate
- failure and retry behavior
- safety and policy compliance

## Common pattern

- build a labeled evaluation set
- test both happy path and edge cases
- measure quality per tool call pattern
- track regressions over time

## Interview guidance

> A production AI system is only as good as its evaluation loop. Good prompts and tools alone are not enough if you cannot measure failure modes and regressions.

## Related notes

- [What agents are](what-are-agents.md)
- [RAG](rag.md)
- [MCP](mcp.md)
