---
title: "Patterns overview"
tags: ["dsa","patterns"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Patterns overview

## When to use which pattern

| Pattern | Use when | Typical complexity |
| --- | --- | --- |
| Two pointers | sorted arrays, in-place scanning | O(n) |
| Sliding window | contiguous subarray/substring constraints | O(n) |
| Binary search | sorted data or monotonic predicate | O(log n) |
| BFS / DFS | trees, graphs, connectivity, shortest path | O(V + E) |
| DP | overlapping subproblems and optimal substructure | O(n^2) or worse |
| Backtracking | enumeration with pruning | often exponential |
| Heap | top-k, smallest/largest, priority scheduling | O(n log n) |
| Monotonic stack | next greater, previous smaller, histogram | O(n) |
| Union-find | connectivity / cycle detection | almost O(n ?(n)) |
| Trie | prefix matching, dictionary lookups | O(word length) |

## Interview mindset

- Identify the structure first: sequence, sorted data, graph, or overlapping subproblem.
- Separate the brute-force idea from the optimized idea.
- Explain the invariant that makes the optimization correct.
- Mention edge cases and constraints before coding.

## 3 core practice habits

1. Solve the problem at least two ways: brute force and optimized.
2. State the invariant explicitly: the key property that stays true after each step.
3. Verify complexity before writing final code.

## Related notes

- [Two pointers](two-pointers.md)
- [Sliding window](sliding-window.md)
- [Binary search](binary-search.md)
- [BFS / DFS](bfs-dfs.md)
