---
title: "RAG"
tags: ["agentic-ai","rag"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# RAG

## Definition

Retrieval-Augmented Generation (RAG) brings relevant external documents into the prompt before generating a response.

## Why it matters

It reduces hallucination, improves factual grounding, and allows access to private or recent information outside the base model knowledge.

## Typical pipeline

1. Chunk documents
2. Embed chunks
3. Store in a vector or hybrid index
4. Retrieve top matches for the query
5. Inject results into the model context
6. Generate a grounded answer

## Trade-offs

- Better grounding, but more latency and cost
- Retrieval quality matters more than model size in many production cases
- Chunking strategy can dramatically affect results

## Related notes

- [What agents are](what-are-agents.md)
- [Tool calling](tool-calling.md)
- [MCP](mcp.md)
