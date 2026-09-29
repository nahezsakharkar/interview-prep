---
title: "Complexity cheat sheet"
tags: ["dsa","complexity"]
difficulty: easy
status: revised
last_reviewed: 2026-09-30
---

# Complexity cheat sheet

## Core idea

Big O describes how runtime or memory usage grows with input size. In interviews, the goal is to be precise about the worst case and to explain the trade-off clearly.

## Common complexity classes

| Complexity | Typical meaning | Common examples |
| --- | --- | --- |
| O(1) | Constant time | hash lookup, array index access |
| O(log n) | Binary reduction | binary search |
| O(n) | Linear scan | loop over array |
| O(n log n) | Efficient divide-and-conquer or sorting | merge sort, heap sort |
| O(n^2) | Nested loops | naive matrix traversal |
| O(n * m) | Two-dimensional DP or nested loops | grid DP |
| O(2^n) | Exponential growth | subset generation |
| O(n!) | factorial growth | brute-force permutations |

## Best / average / worst

- Binary search: best O(1), average O(log n), worst O(log n)
- Hash map lookup: average O(1), worst O(n) under pathological collisions
- Quick sort: average O(n log n), worst O(n^2)
- Heap push/pop: O(log n) worst, amortized okay for repeated operations
- BFS/DFS on a graph: O(V + E)

## Interview rules of thumb

- If you can reduce the search space by half, think binary search.
- If the problem asks for a subarray or substring under a constraint, think sliding window.
- If the subproblem overlaps, think dynamic programming.
- If you need the smallest/largest value repeatedly, think heap.
- If you need to process connected groups, think union-find or DFS.

## Space complexity checklist

- Recursion uses stack space: O(h) for tree height or O(n) in worst case.
- DP tables often use O(n) or O(n * m) extra memory.
- Hash maps / sets use O(n) extra memory.
- In-place algorithms may use O(1) extra memory.

## Example

```ts
function findMax(nums: number[]): number {
  let max = nums[0];

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] > max) {
      max = nums[i];
    }
  }

  return max;
}
```

Time: O(n)
Space: O(1)

## Related notes

- [Patterns overview](patterns-overview.md)
- [Two pointers](two-pointers.md)
- [Sliding window](sliding-window.md)
