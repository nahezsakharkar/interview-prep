---
title: "Sliding window"
tags: ["dsa","sliding-window"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Sliding window

## Definition

Sliding window maintains a moving range over an array or string and updates it as constraints change. It is ideal when the problem asks for a contiguous segment that satisfies a condition.

## Typical complexity

- Best: O(n)
- Average: O(n)
- Worst: O(n)
- Space: O(1) to O(k) depending on the state tracked

## Problem 1: Maximum sum subarray of size K

```ts
function maxSumSubarray(nums: number[], k: number): number {
  let windowSum = 0;
  for (let i = 0; i < k; i++) {
    windowSum += nums[i];
  }

  let maxSum = windowSum;
  for (let i = k; i < nums.length; i++) {
    windowSum += nums[i] - nums[i - k];
    maxSum = Math.max(maxSum, windowSum);
  }

  return maxSum;
}
```

Time: O(n), space: O(1).

## Problem 2: Longest substring without repeating characters

```ts
function lengthOfLongestSubstring(s: string): number {
  const seen = new Map<string, number>();
  let left = 0;
  let longest = 0;

  for (let right = 0; right < s.length; right++) {
    const ch = s[right];
    if (seen.has(ch)) {
      left = Math.max(left, seen.get(ch)! + 1);
    }
    seen.set(ch, right);
    longest = Math.max(longest, right - left + 1);
  }

  return longest;
}
```

Time: O(n), space: O(min(n, k)) where k is the alphabet size or distinct characters.

## Problem 3: Minimum window substring

```ts
function minWindow(s: string, t: string): string {
  if (t.length > s.length) return '';

  const need = new Map<string, number>();
  for (const ch of t) {
    need.set(ch, (need.get(ch) ?? 0) + 1);
  }

  let have = 0;
  let required = need.size;
  const window = new Map<string, number>();
  let left = 0;
  let bestStart = -1;
  let bestLen = Number.MAX_SAFE_INTEGER;

  for (let right = 0; right < s.length; right++) {
    const ch = s[right];
    window.set(ch, (window.get(ch) ?? 0) + 1);
    if (need.has(ch) && window.get(ch) === need.get(ch)) {
      have += 1;
    }

    while (have === required) {
      const len = right - left + 1;
      if (len < bestLen) {
        bestLen = len;
        bestStart = left;
      }

      const leftChar = s[left];
      if (window.has(leftChar)) {
        const leftCount = (window.get(leftChar) ?? 1) - 1;
        window.set(leftChar, leftCount);
        if (need.has(leftChar) && leftCount < (need.get(leftChar) ?? 0)) {
          have -= 1;
        }
      }
      left += 1;
    }
  }

  return bestStart === -1 ? '' : s.slice(bestStart, bestStart + bestLen);
}
```

Time: O(n), space: O(k) for the target character map.

## Common mistakes

- Forgetting to shrink the window after it becomes valid.
- Recomputing the window sum from scratch instead of using the moving invariant.
- Not tracking current counts when multiple characters repeat.

## Related notes

- [Two pointers](two-pointers.md)
- [Binary search](binary-search.md)
- [Patterns overview](patterns-overview.md)
