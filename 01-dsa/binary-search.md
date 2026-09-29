---
title: "Binary search"
tags: ["dsa","binary-search"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Binary search

## Definition

Binary search works on sorted data by repeatedly halving the search space. It is one of the fastest ways to find a target or a boundary when the answer space is monotonic.

## Typical complexity

- Best: O(1)
- Average: O(log n)
- Worst: O(log n)
- Space: O(1)

## Problem 1: Search in sorted array

```ts
function binarySearch(nums: number[], target: number): number {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (nums[mid] === target) return mid;
    if (nums[mid] < target) left = mid + 1;
    else right = mid - 1;
  }

  return -1;
}
```

## Problem 2: Search insert position

```ts
function searchInsert(nums: number[], target: number): number {
  let left = 0;
  let right = nums.length;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);
    if (nums[mid] < target) left = mid + 1;
    else right = mid;
  }

  return left;
}
```

## Problem 3: First bad version

```ts
function firstBadVersion(n: number, isBad: (version: number) => boolean): number {
  let left = 1;
  let right = n;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);
    if (isBad(mid)) right = mid;
    else left = mid + 1;
  }

  return left;
}
```

## Common mistakes

- Forgetting the sorted prerequisite.
- Using the wrong equality and boundary condition.
- Confusing search for exact value versus first valid/invalid boundary.

## Related notes

- [Two pointers](two-pointers.md)
- [Complexity cheat sheet](complexity-cheat-sheet.md)
- [Patterns overview](patterns-overview.md)
