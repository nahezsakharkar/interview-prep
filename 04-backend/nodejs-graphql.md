---
title: "Advanced Backend: Node.js and GraphQL"
tags: ["backend","nodejs","graphql"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Node.js and GraphQL

## 1. Node.js Internals

Node.js is a JavaScript runtime built on Chrome's V8 engine. Its core strength is **non-blocking I/O**.

### The Event Loop
The event loop allows Node.js to perform non-blocking I/O operations by offloading them to the system kernel whenever possible.
- **Phases**: Timers $\rightarrow$ Pending Callbacks $\rightarrow$ Idle/Prepare $\rightarrow$ Poll $\rightarrow$ Check $\rightarrow$ Close Callbacks.
- **Microtask Queue**: `process.nextTick` and `Promise` callbacks are executed immediately after the current operation, before the event loop moves to the next phase.

### Streams and Buffer
For handling large amounts of data (e.g., uploading a 1GB file), Node.js uses **Streams** to process data in chunks.
- **Readable**: Data source.
- **Writable**: Data destination.
- **Duplex**: Both (e.g., TCP socket).
- **Transform**: Modifies data as it passes through (e.g., Gzip compression).

## 2. GraphQL

GraphQL is a query language for APIs and a runtime for fulfilling those queries with existing data.

### Core Concepts
- **Schema**: A strongly typed definition of the data available.
- **Query**: Client requests exactly what they need (no over-fetching).
- **Mutation**: Used to create, update, or delete data.
- **Resolver**: A function that fetches the data for a specific field in the schema.

### GraphQL vs REST

| Feature | REST | GraphQL |
| :--- | :--- | :--- |
| **Data Fetching** | Multiple endpoints (`/users`, `/posts`) | Single endpoint (`/graphql`) |
| **Payload** | Fixed by server (over-fetching) | Defined by client (precise) |
| **Versioning** | `/v1/`, `/v2/` | Schema evolution (deprecating fields) |
| **Caching** | Native HTTP caching | Complex (requires Client-side cache like Apollo) |

### The N+1 Problem in GraphQL
If a query asks for `users` and their `posts`, a naive resolver will call `getUser()` once and then `getPosts()` for every single user.
- **Solution**: Use **DataLoader**. It batches and caches requests within a single request cycle, turning $N+1$ queries into 2 queries.

## 3. Interview Q&A

**Q: When would you choose REST over GraphQL?**
**A**: 
1. When the API is public and needs simple HTTP caching.
2. When the data model is very simple and doesn't require complex nested relationships.
3. When the client is very simple and doesn't benefit from custom queries.

**Q: How does Node.js handle CPU-intensive tasks?**
**A**: Since Node is single-threaded, CPU-intensive tasks block the event loop. Solutions include:
1. **Worker Threads**: Use the `worker_threads` module for true parallelism.
2. **Child Processes**: Spawn separate OS processes.
3. **Offloading**: Move the task to a background worker (e.g., Celery, RabbitMQ).

## Related notes

- [Spring Boot internals](04-backend/spring-boot-internals.md)
- [REST design](04-backend/rest-design.md)
