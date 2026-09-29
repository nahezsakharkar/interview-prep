---
title: "Monotonic stack"
tags: ["dsa","monotonic-stack"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Monotonic stack

## Definition

A monotonic stack keeps its elements in sorted order (increasing or decreasing) so you can answer nearest-greater or nearest-smaller queries efficiently.

## Typical complexity

- Best: O(n)
- Average: O(n)
- Worst: O(n)
- Space: O(n)

## Problem 1: Daily temperatures

```ts
function dailyTemperatures(temperatures: number[]): number[] {
  const result = new Array(temperatures.length).fill(0);
  const stack: number[] = [];

  for (let i = temperatures.length - 1; i >= 0; i--) {
    while (stack.length && temperatures[i] >= temperatures[stack[stack.length - 1]]) {
      stack.pop();
    }

    result[i] = stack.length ? stack[stack.length - 1] - i : 0;
    stack.push(i);
  }

  return result;
}
```

This is a classic next-greater-element pattern.

## Problem 2: Largest rectangle in histogram

```ts
function largestRectangleArea(heights: number[]): number {
  const stack: number[] = [];
  let max = 0;

  for (let i = 0; i <= heights.length; i++) {
    const curr = i === heights.length ? 0 : heights[i];
    while (stack.length && curr < heights[stack[stack.length - 1]]) {
      const height = heights[stack.pop()!];
      const width = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      max = Math.max(max, height * width);
    }
    stack.push(i);
  }

  return max;
}
```

## Problem 3: Next greater element

```ts
function nextGreaterElement(nums: number[]): number[] {
  const result = new Array(nums.length).fill(-1);
  const stack: number[] = [];

  for (let i = nums.length - 1; i >= 0; i--) {
    while (stack.length && nums[i] >= stack[stack.length - 1]) {
      stack.pop();
    }

    result[i] = stack.length ? stack[stack.length - 1] : -1;
    stack.push(nums[i]);
  }

  return result;
}
```

## Common mistakes

- Not maintaining monotonic order strictly or non-strictly depending on duplicates.
- Pop too early or too late while answering the nearest greater/smaller query.
- Forgetting to handle empty stack cases.

## Related notes

- [Heap](heap.md)
- [BFS / DFS](bfs-dfs.md)
- [Patterns overview](patterns-overview.md)
