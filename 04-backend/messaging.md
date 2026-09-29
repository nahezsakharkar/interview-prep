---
title: "Messaging Systems"
tags: ["backend"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Messaging Systems

Tags: #backend #async
Difficulty: Medium
Status: Learning

## Definition

Messaging systems decouple producers and consumers so work can happen asynchronously across services.

## Why it matters / when to use

They are useful for resilience, load smoothing, retries, and background job processing.

## How it works

Queues and topics allow producers to send messages without waiting on consumers. Consumers can process at their own pace and retry failures.

## Code example

```ts
const queue: string[] = [];

function publish(msg: string) {
  queue.push(msg);
}

function consume() {
  const next = queue.shift();
  if (next) console.log(`Processing: ${next}`);
}
```

## Time and space complexity

Queue operations are usually O(1) average for push and pop in a simple implementation.

## Common mistakes and pitfalls

- Ignoring idempotency for retries
- Assuming message delivery is always instant
- Forgetting to handle poison messages and retry budgets

## Interview questions

### Q: Why use a queue instead of a direct synchronous call?
Model answer: A queue helps isolate failures, smooth spikes in traffic, and move expensive work off the critical request path.

## Related topics

- [Caching strategies](caching.md)
- [Microservices patterns](microservices.md)
- [CI/CD principles](../08-devops/ci-cd.md)
