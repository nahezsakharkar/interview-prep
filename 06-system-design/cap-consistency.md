---
title: "CAP, PACELC and Consistency"
tags: ["system-design","consistency","cap"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# CAP, PACELC and Consistency

## 1. The CAP Theorem

The CAP theorem states that in the presence of a **Network Partition (P)**, a distributed system must choose between **Consistency (C)** and **Availability (A)**.

### The components
- **Consistency (C)**: Every read receives the most recent write or an error.
- **Availability (A)**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
- **Partition Tolerance (P)**: The system continues to operate despite an arbitrary number of messages being dropped or delayed by the network.

### The "Choose Two" Misconception
It is often said that you "pick two," but since network partitions are inevitable in distributed systems, **P is not optional**. The real choice occurs only during a partition:
- **CP (Consistency/Partition Tolerance)**: The system returns an error or times out if it cannot guarantee the latest data. (Example: MongoDB, HBase, Zookeeper).
- **AP (Availability/Partition Tolerance)**: The system returns the best available data, even if it might be stale. (Example: Cassandra, DynamoDB).

## 2. The PACELC Theorem

PACELC extends CAP by describing how the system behaves when there is **no partition**.

- **P (Partition)** $\rightarrow$ **A (Availability)** or **C (Consistency)**: During a partition, do you prioritize availability or consistency?
- **E (Else)** $\rightarrow$ **L (Latency)** or **C (Consistency)**: When the system is running normally (no partition), do you prioritize low latency or strong consistency?

### Examples
- **DynamoDB/Cassandra**: Often configured as **PA/EL**. During a partition, they favor Availability. Normally, they favor low Latency (eventual consistency).
- **Zookeeper/Etcd**: Often **PC/SC**. During a partition, they favor Consistency. Normally, they favor strong Consistency over latency.

## 3. Consistency Models

| Model | Guarantee | Trade-off | Typical Use Case |
| :--- | :--- | :--- | :--- |
| **Strong** | Reads always see the latest write. | High latency, low availability during partitions. | Bank balances, stock inventory. |
| **Eventual** | Replicas will converge eventually. | Low latency, risk of stale reads. | Social media feeds, DNS. |
| **Causal** | Operations that are causally related are seen in order. | Moderate complexity. | Chat history, comment threads. |
| **Read-Your-Writes** | A user always sees their own latest update. | Requires session stickiness or specific routing. | User profile updates. |

## 4. Interview Framing

When asked about consistency in a design case:
1. **Identify the "Critical Path"**: Does this feature require absolute correctness (e.g., Payment) or can it tolerate a few seconds of lag (e.g., Like count)?
2. **Apply PACELC**: Explain that you are choosing $\text{C}$ over $\text{A}$ during a partition to prevent double-spending, and $\text{C}$ over $\text{L}$ normally to ensure the user sees their balance immediately.
3. **Mitigation**: If choosing Eventual Consistency, explain how you handle conflicts (e.g., Last-Write-Wins, Vector Clocks, CRDTs).

## Related notes

- [Scalability basics](scalability-basics.md)
- [Sharding and queues](sharding-and-queues.md)
- [Rate limiter](rate-limiter.md)
