---
title: "Greedy Algorithms"
tags: ["dsa","greedy","proof"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Greedy Algorithms

## Definition

A greedy algorithm makes the locally best choice at each step, hoping that those local choices lead to a globally optimal answer. Greedy is often efficient, but it is only correct when the problem has a safe greedy-choice property and a compatible optimal-substructure property.

## When to use

- Interval scheduling / activity selection.
- Canonical coin-change problems where the coin system has a standard greedy property.
- Huffman coding or other data-compression problems with a well-posed exchange argument.
- Problems where a clear priority rule is obvious and can be supported by a proof.

## Why greedy can fail

Greedy often looks attractive, but it does not work for all optimization problems. Counterexamples such as coin systems with non-canonical coin denominations or weighted scheduling problems show why a greedy proof matters.

## Complexity reference

| Pattern | Typical time | Typical space | Notes |
| --- | --- | --- | --- |
| Sort + scan | O(n log n) | O(1) or O(n) depending on implementation | Common for interval scheduling |
| Priority queue / heap | O(n log n) | O(n) | Good when multiple candidate choices are active |
| Single-pass with a fixed rule | O(n) | O(1) | Best-case when the greedy decision is clear |

## Problem: Activity selection

**Problem:** Given a list of intervals `[start, end)`, return the maximum number of non-overlapping activities. Choose the next activity with the earliest finishing time.

**Pattern:** Greedy by earliest finish time.

### Proof idea

If there are two activities with the same earliest start time, the one that finishes earlier can only leave more room for future activities. Choosing the earliest finishing time cannot reduce the maximum possible count, because it leaves the maximum remaining slack.

### TypeScript solution

```ts
function activitySelection(intervals: number[][]): number[][] {
  const sorted = [...intervals].sort((a, b) => a[1] - b[1] || a[0] - b[0]);
  const chosen: number[][] = [];
  let lastEnd = Number.NEGATIVE_INFINITY;

  for (const [start, end] of sorted) {
    if (start >= lastEnd) {
      chosen.push([start, end]);
      lastEnd = end;
    }
  }

  return chosen;
}

console.log(activitySelection([
  [1, 3],
  [2, 4],
  [3, 5],
  [4, 6],
  [6, 8],
]));
```

Expected output: `[[1, 3], [4, 6], [6, 8]]` or another equivalent set depending on the interval ordering and tie-break handling. The important property is maximum count and non-overlap.

### Java solution (Java 17+)

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

class Solution {
    static List<int[]> activitySelection(int[][] intervals) {
        Arrays.sort(intervals, Comparator.comparingInt(a -> a[1]));
        List<int[]> chosen = new ArrayList<>();
        int lastEnd = Integer.MIN_VALUE;

        for (int[] interval : intervals) {
            int start = interval[0];
            int end = interval[1];
            if (start >= lastEnd) {
                chosen.add(new int[] { start, end });
                lastEnd = end;
            }
        }

        return chosen;
    }

    public static void main(String[] args) {
        int[][] intervals = {
            {1, 3},
            {2, 4},
            {3, 5},
            {4, 6},
            {6, 8}
        };
        System.out.println(Arrays.deepToString(activitySelection(intervals).toArray()));
    }
}
```

Expected output: `[[1, 3], [4, 6], [6, 8]]` or a logically equivalent schedule with same count.

## Complexity / trade-offs

- Sorting the intervals is O(n log n); the greedy scan is O(n).
- Overall complexity is O(n log n) time and O(1) auxiliary space beyond the chosen list.
- This greedy strategy is correct for interval scheduling because the earliest finish time leaves maximum room for remaining intervals.
- For other optimization problems, a greedy rule needs a proof or an exchange argument; otherwise it can be wrong.

## Common mistakes

- Applying greedy without verifying that the chosen local rule preserves optimality.
- Using a wrong sort key, such as earliest start time instead of earliest finish time.
- Ignoring tie-breaking rules and claiming one exact schedule is the only valid solution.
- Assuming all coin systems are greedy-safe; standard coins are often greedy-safe, but some denominations are not.
- Forgetting to state the exchange argument when asked to justify the greedy choice.

## Interview questions

### Q1: How do you know when greedy is appropriate?
**Model answer:** Only after checking the problem's greedy-choice property and optimal-substructure. Without a proof or exchange argument, the local choice may be incorrect.

### Q2: Why sort by end time in activity selection?
**Model answer:** Selecting the interval that ends first leaves the maximum remaining time for later choices and cannot reduce the maximum possible count.

### Q3: Is greedy always faster than DP?
**Model answer:** Usually yes for the right problem, but not always. Greedy reduces complexity by avoiding all states; DP is more general and is required when local choices are not independent.

### Q4: What is an exchange argument?
**Model answer:** It shows that any optimal solution can be transformed so that it matches the greedy choice without reducing the value of the solution.

### Q5: Why are some coin-change problems not greedy-safe?
**Model answer:** A canonical coin system like US coins is greedy-safe for many practical cases, but a non-canonical set may require dynamic programming or a different choice rule.

### Q6: Can greedy work on weighted jobs or scheduling with penalties?
**Model answer:** Not in general. Weighted job scheduling and many resource-allocation problems require DP or alternative optimization methods because the local choice is not always globally safe.

### Q7: What problem sizes are good for greedy algorithms?
**Model answer:** Greedy is often attractive for linear-time or O(n log n) scan problems where the sort key and safety proof are simple and direct.

### Q8: What is the difference between greedy and dynamic programming?
**Model answer:** DP explores states and subproblems; greedy commits to a locally optimal choice that is justified by proof. DP is more general and often more robust when greedy does not apply.

### Q9: How do you explain a greedy proof in an interview?
**Model answer:** State the greedy choice, then give a short exchange argument that any optimal solution can be rearranged to use the same choice without losing objective value.

### Q10: What is the trade-off of greedy algorithms?
**Model answer:** They are fast and elegant when correct, but the proof burden is higher and the logic is less general than DP or graph-based optimization.

## Related notes

- [Dynamic programming](dynamic-programming.md)
- [Binary search](binary-search.md)
- [Graph algorithms](graph-algorithms.md)
- [Complexity cheat sheet](complexity-cheat-sheet.md)
