---
title: "Intervals and Merge"
tags: ["dsa","intervals","greedy"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Intervals and Merge

## Core idea

An interval is a range like `[start, end]`. For coding problems, the most common approach is:

- sort by start time
- merge overlapping or touching intervals
- scan once to build the answer

The exact semantics matter: some problems treat intervals as inclusive, some as half-open. Always confirm the contract before coding.

## Pattern 1: merge overlapping intervals

### TypeScript

```ts
function mergeIntervals(intervals: number[][]): number[][] {
  if (intervals.length <= 1) return intervals;

  intervals.sort((a, b) => a[0] - b[0]);
  const merged: number[][] = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    const current = intervals[i];
    const last = merged[merged.length - 1];

    if (current[0] <= last[1]) {
      last[1] = Math.max(last[1], current[1]);
    } else {
      merged.push(current);
    }
  }

  return merged;
}

console.log(mergeIntervals([[1, 3], [2, 6], [8, 10], [15, 18]]));
// [[1, 6], [8, 10], [15, 18]]
```

### Java

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class IntervalMerge {
    public static List<int[]> mergeIntervals(int[][] intervals) {
        if (intervals == null || intervals.length <= 1) {
            return Arrays.stream(intervals == null ? new int[0][] : intervals)
                    .map(arr -> new int[]{arr[0], arr[1]})
                    .toList();
        }

        Arrays.sort(intervals, Comparator.comparingInt(a -> a[0]));
        List<int[]> merged = new ArrayList<>();
        merged.add(new int[]{intervals[0][0], intervals[0][1]});

        for (int i = 1; i < intervals.length; i++) {
            int[] current = intervals[i];
            int[] last = merged.get(merged.size() - 1);

            if (current[0] <= last[1]) {
                last[1] = Math.max(last[1], current[1]);
            } else {
                merged.add(new int[]{current[0], current[1]});
            }
        }

        return merged;
    }

    public static void main(String[] args) {
        int[][] intervals = {{1, 3}, {2, 6}, {8, 10}, {15, 18}};
        System.out.println(mergeIntervals(intervals));
    }
}
```

### Complexity

- Time: O(n log n) best/average/worst because of sorting
- Space: O(n) worst for the merged output

## Pattern 2: insert an interval

```ts
function insertInterval(intervals: number[][], newInterval: number[]): number[][] {
  const result: number[][] = [];

  for (let i = 0; i < intervals.length; i++) {
    const current = intervals[i];

    if (current[1] < newInterval[0]) {
      result.push(current);
    } else if (current[0] > newInterval[1]) {
      result.push(newInterval);
      newInterval = current;
    } else {
      newInterval = [
        Math.min(newInterval[0], current[0]),
        Math.max(newInterval[1], current[1]),
      ];
    }
  }

  result.push(newInterval);
  return result;
}
```

Example:

```ts
const intervals = [[1, 3], [6, 9]];
console.log(insertInterval(intervals, [2, 5]));
// [[1, 5], [6, 9]]
```

### Complexity

- Time: O(n) best/average/worst when the intervals array is already sorted and we do a single pass
- Space: O(n) worst for the output array

## Pattern 3: interval scheduling / activity selection

When the goal is to maximize the number of non-overlapping intervals, sort by end time and greedily take the earliest finishing job.

```ts
function maxNonOverlappingIntervals(intervals: number[][]): number[] {
  const sorted = [...intervals].sort((a, b) => a[1] - b[1] || a[0] - b[0]);
  const chosen: number[] = [];
  let lastEnd = -Infinity;

  for (const [start, end] of sorted) {
    if (start >= lastEnd) {
      chosen.push(start, end);
      lastEnd = end;
    }
  }

  return chosen;
}
```

### Complexity

- Time: O(n log n) best/average/worst because of sorting
- Space: O(n) worst for the result array

## Common interview traps

- Mixing inclusive and exclusive interval boundaries.
- Forgetting to sort by start time before merging.
- Using `current[0] <= last[1]` instead of checking the exact rule for the problem.
- Not handling touching intervals correctly, such as `[1, 2]` and `[2, 5]`.

## When to use this pattern

Choose interval logic when the problem asks about:

- meeting rooms
- merge or overlap detection
- insertion of a range into a sorted list
- scheduling under resource constraints
- booking calendars or availability windows

## Related notes

- [Greedy algorithms](greedy.md)
- [Sorting algorithms](sorting.md)
- [Graph algorithms](graph-algorithms.md)
- [Patterns overview](patterns-overview.md)
