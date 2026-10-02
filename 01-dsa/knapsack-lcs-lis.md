---
title: "Knapsack, LCS, and LIS"
tags: ["dsa","dynamic-programming","knapsack","lcs","lis"]
difficulty: hard
status: learning
last_reviewed: 2026-10-02
---

# Knapsack, LCS, and LIS

## Definition

These are classic dynamic-programming patterns:

- 0/1 knapsack chooses items with a weight limit to maximize value.
- Longest common subsequence (LCS) finds the longest common subsequence across two strings.
- Longest increasing subsequence (LIS) finds the longest strictly increasing subsequence in an array.

## Why they matter

These patterns frequently appear in coding interviews because they test state design, recurrence logic, and the difference between greedy and dynamic programming.

## Complexity reference

| Pattern | Time | Space | Typical recurrence |
| --- | --- | --- | --- |
| 0/1 knapsack | O(n * W) | O(n * W) or O(W) | `dp[i][w] = max(dp[i-1][w], dp[i-1][w-weight[i]] + value[i])` |
| LCS | O(m * n) | O(m * n) or O(min(m, n)) for rolling arrays | If chars match, add 1; else take max of left/up |
| LIS | O(n²) DP or O(n log n) patience sorting | O(n) or O(n²) | `dp[i] = 1 + max(dp[j])` for `j < i` and `a[j] < a[i]` |

The best, average, and worst cases are usually the same for these canonical DP forms, unless an optimization like patience sorting reduces the LIS time to O(n log n).

## Problem 1: 0/1 knapsack

**Problem:** Given item weights and values, maximize total value without exceeding capacity `W`.

**Pattern:** DP over items and capacity.

### TypeScript solution

```ts
function knapsack01(weights: number[], values: number[], capacity: number): number {
  const dp = Array.from({ length: weights.length + 1 }, () => Array(capacity + 1).fill(0));

  for (let i = 1; i <= weights.length; i++) {
    for (let w = 0; w <= capacity; w++) {
      if (weights[i - 1] <= w) {
        dp[i][w] = Math.max(
          dp[i - 1][w],
          values[i - 1] + dp[i - 1][w - weights[i - 1]]
        );
      } else {
        dp[i][w] = dp[i - 1][w];
      }
    }
  }

  return dp[weights.length][capacity];
}

console.log(knapsack01([2, 3, 4], [3, 4, 5], 5));
```

Expected output: `7` (choose items with weights `2 + 3` and value `3 + 4`).

### Java solution (Java 17+)

```java
import java.util.Arrays;

class Solution {
    static int knapsack01(int[] weights, int[] values, int capacity) {
        int[][] dp = new int[weights.length + 1][capacity + 1];

        for (int i = 1; i <= weights.length; i++) {
            for (int w = 0; w <= capacity; w++) {
                if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(
                        dp[i - 1][w],
                        values[i - 1] + dp[i - 1][w - weights[i - 1]]
                    );
                } else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }

        return dp[weights.length][capacity];
    }

    public static void main(String[] args) {
        int[] weights = {2, 3, 4};
        int[] values = {3, 4, 5};
        System.out.println(knapsack01(weights, values, 5));
    }
}
```

Expected output: `7`.

### Dry run

For capacity `5`, the DP table eventually stores the best value for each `itemCount × remainingCapacity` state. The value at `dp[3][5]` is the maximum value achievable with the first three items under a total weight of 5.

## Problem 2: Longest common subsequence (LCS)

**Problem:** Given two strings, find the length of the longest common subsequence.

**Pattern:** DP over prefixes.

### TypeScript solution

```ts
function longestCommonSubsequence(a: string, b: string): number {
  const dp = Array.from({ length: a.length + 1 }, () => Array(b.length + 1).fill(0));

  for (let i = 1; i <= a.length; i++) {
    for (let j = 1; j <= b.length; j++) {
      if (a[i - 1] === b[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1;
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }

  return dp[a.length][b.length];
}

console.log(longestCommonSubsequence('abcde', 'ace'));
```

Expected output: `3` (LCS is `ace` or `abc`/`acd` depending on the chosen subsequence, but the length is 3).

### Java solution (Java 17+)

```java
class Solution {
    static int longestCommonSubsequence(String a, String b) {
        int[][] dp = new int[a.length() + 1][b.length() + 1];

        for (int i = 1; i <= a.length(); i++) {
            for (int j = 1; j <= b.length(); j++) {
                if (a.charAt(i - 1) == b.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[a.length()][b.length()];
    }

    public static void main(String[] args) {
        System.out.println(longestCommonSubsequence("abcde", "ace"));
    }
}
```

Expected output: `3`.

## Problem 3: Longest increasing subsequence (LIS)

**Problem:** Find the length of the longest strictly increasing subsequence in an array.

**Pattern:** DP or patience sorting.

### TypeScript solution (O(n²) DP)

```ts
function lengthOfLIS(nums: number[]): number {
  if (nums.length === 0) return 0;

  const dp = Array(nums.length).fill(1);
  let best = 1;

  for (let i = 1; i < nums.length; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[j] < nums[i]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
    best = Math.max(best, dp[i]);
  }

  return best;
}

console.log(lengthOfLIS([10, 9, 2, 5, 3, 7, 101, 18]));
```

Expected output: `4` (for example, `[2, 3, 7, 101]` or `[2, 3, 7, 18]`).

### Java solution (Java 17+)

```java
class Solution {
    static int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        int[] dp = new int[nums.length];
        Arrays.fill(dp, 1);
        int best = 1;

        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            best = Math.max(best, dp[i]);
        }

        return best;
    }

    public static void main(String[] args) {
        int[] nums = {10, 9, 2, 5, 3, 7, 101, 18};
        System.out.println(lengthOfLIS(nums));
    }
}
```

Expected output: `4`.

### O(n log n) optimization

An array `tails` stores the smallest possible tail value for each subsequence length. When iterating the numbers, use binary search to find the first `tails[index] >= num` and replace it. This gives O(n log n) with O(n) space and is a classic interview optimization.

## Complexity and trade-offs

- 0/1 knapsack is O(n * W) time and O(n * W) space in the classic full table; it can often be reduced to O(W) space by storing only the previous row.
- LCS is O(m * n) time and O(m * n) space in the standard 2D DP table; rolling arrays can reduce space to O(min(m, n)).
- LIS has a simple O(n²) DP solution; the `tails` optimization reduces it to O(n log n).
- The DP form is more general and easier to prove; the optimization is faster but may be less obvious without careful design.

## Common mistakes

- Not defining the state precisely; if the state is unclear, the recurrence will be unclear too.
- Confusing subsequence with substring; LCS permits skipping characters but keeps order, while substring requires contiguous positions.
- Forgetting the zero-weight or zero-capacity edge cases in knapsack.
- Using “strictly increasing” when the problem allows duplicates or equal values; define the rule explicitly.
- Over-optimizing with the O(n log n) LIS trick before clearly understanding the DP version.

## Interview questions

### Q1: What makes 0/1 knapsack a DP problem?
**Model answer:** The optimal choice for an item depends on whether we include it, and the remaining capacity changes the future problem. This creates overlapping subproblems and an optimal-substructure recurrence.

### Q2: What is the difference between 0/1 and unbounded knapsack?
**Model answer:** In 0/1 knapsack, each item can be taken at most once. In unbounded knapsack, the same item type may be chosen repeatedly, changing the recurrence.

### Q3: How do you derive the LCS recurrence?
**Model answer:** If the last characters match, extend the sequence by 1; otherwise take the best result from either dropping the last character of the first or second string.

### Q4: Why is LIS not the same as LCS?
**Model answer:** LCS compares two sequences; LIS finds the longest increasing order within one sequence. The state design differs, even though both are DP patterns.

### Q5: Why is the LIS O(n log n) optimization valid?
**Model answer:** `tails[k]` stores the smallest possible tail value for an increasing subsequence of length `k + 1`, enabling binary-search insertion while preserving the possibility of extending the subsequence.

### Q6: Which problems need a full 2D DP table?
**Model answer:** Problems with two sequence dimensions, such as LCS, edit distance, and many string-to-string alignment tasks, often need the full table to track prefixes.

### Q7: Can knapsack be solved greedily?
**Model answer:** Not in general. Greedy can fail even on simple counterexamples. DP is the standard safe choice when the objective is value under a capacity constraint.

### Q8: What is the role of base cases?
**Model answer:** Base cases define the answer when no items are left or the available capacity/truncated strings are empty. Without them, the recurrence cannot bootstrap correctly.

### Q9: What is the effect of duplicates in LIS?
**Model answer:** The exact problem contract decides whether equal values are allowed. A strictly increasing subsequence forbids equal values; a non-decreasing version uses `<=` instead of `<` in the recurrence.

### Q10: Which of these patterns is usually the hardest to prove in an interview?
**Model answer:** LCS and knapsack often require careful recurrence explanation, while LIS is easier once the state and transition are clear. The hardest part is usually stating the correct state rather than coding the iteration itself.

## Related notes

- [Dynamic programming](dynamic-programming.md)
- [Greedy algorithms](greedy.md)
- [Sorting algorithms](sorting.md)
- [Complexity cheat sheet](complexity-cheat-sheet.md)
