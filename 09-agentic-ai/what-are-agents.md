---
title: "What agents are"
tags: ["agentic-ai","agents"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# What agents are

## Definition

An agent is a system that can reason, choose actions, invoke tools, and iterate until the task is complete or a stop condition is reached.

## What makes it different from a simple prompt?

- It can call external tools
- It can inspect intermediate results
- It can plan a sequence of steps instead of answering in one shot
- It often works with memory and guardrails

## Example workflow

```mermaid
flowchart TD
	goal[User goal] --> reason[Model reasons about next step]
	reason --> action{Need an action?}
	action -->|Yes| tool[Invoke a permitted tool]
	tool --> observe[Inspect result]
	observe --> complete{Goal met or stop condition?}
	complete -->|No| reason
	complete -->|Yes| answer[Return answer]
	action -->|No| answer
```

## Interview guidance

- Agents are not magic; they need explicit boundaries and good evaluation.
- Tool use is usually where reliability comes from.
- A good agent design clearly separates planning, execution, and verification.

## Related notes

- [Tool calling](tool-calling.md)
- [RAG](rag.md)
- [Memory and guardrails](memory-and-guardrails.md)
