---
title: "Computer Architecture"
tags: ["system-design"]
difficulty: hard
status: learning
last_reviewed: 2026-09-30
---

 Computer Architecture

Tags: #cs #architecture
Difficulty: Medium
Status: Learning

## Definition

Computer architecture studies the organization of processors, memory, storage, and data flow inside a machine.

## Why it matters / when to use

It explains performance patterns like caching, memory locality, and instruction execution.

## How it works

CPUs interact with registers, caches, RAM, and storage. Better locality improves throughput and reduces latency.

## Code example

```ts
const values = [1, 2, 3, 4, 5];
console.log(values[0] + values[1]);
```

## Time and space complexity

This topic is usually discussed in terms of throughput and memory hierarchy rather than Big O.

## Common mistakes and pitfalls

- Ignoring cache locality in performance reasoning
- Treating memory as uniformly fast
- Overlooking how CPUs execute instructions in pipelines

## Interview questions

### Q: Why is cache important?
Model answer: Cache reduces memory access latency by keeping frequently used data near the processor, which improves overall throughput.

## Related topics

- [Operating systems](os.md)
- [Networking](networking.md)
- [OOP and design basics](oop.md)
