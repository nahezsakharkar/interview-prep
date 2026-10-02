---
title: "Sorting Algorithms"
tags: ["dsa","sorting","comparison"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Sorting Algorithms

## Definition

Sorting arranges elements in a defined order, typically ascending or descending. The best choice depends on data size, memory constraints, stability needs, and whether data is already partially ordered.

## Why it matters

- Many algorithms rely on sorted input.
- Frequent in interviews because it tests trade-offs and implementation understanding.
- It reveals whether the candidate understands the cost of comparison vs linear-time specialized methods.

## Common categories

| Algorithm | Best | Average | Worst | Stability | Space | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Bubble sort | O(n) | O(n²) | O(n²) | Stable | O(1) | Simple but slow |
| Selection sort | O(n²) | O(n²) | O(n²) | Not stable | O(1) | Easy to explain; poor for large data |
| Insertion sort | O(n) | O(n²) | O(n²) | Stable | O(1) | Good for nearly sorted arrays |
| Merge sort | O(n log n) | O(n log n) | O(n log n) | Stable | O(n) | Great for predictable performance |
| Quick sort | O(n log n) | O(n log n) | O(n²) | Usually not stable | O(log n) stack average, O(n) worst | Great in practice, but pivot choice matters |
| Heap sort | O(n log n) | O(n log n) | O(n log n) | Not stable | O(1) | In-place but not stable |
| Counting sort | O(n + k) | O(n + k) | O(n + k) | Stable | O(k) | Only when keys are small integers |
| Radix sort | O(d(n + k)) | O(d(n + k)) | O(d(n + k)) | Stable | O(n + k) | Good for fixed-width integer keys |

Here, $k$ refers to the range of possible keys for counting sort; $d$ is the number of digits or passes for radix sort.

## When to choose which one

- Use insertion sort for almost-sorted arrays or very small arrays.
- Use merge sort for deterministic O(n log n) performance and stable order.
- Use quick sort when average-case speed matters and a poor pivot is unlikely.
- Use heap sort when you need in-place O(n log n) without extra arrays.
- Use counting or radix sort when keys are integer-like and bounded.

## Problem: Merge sort

**Problem:** Sort an array in ascending order using merge sort.

**Pattern:** Divide and conquer; sort halves then merge.

### TypeScript solution

```ts
function mergeSort(nums: number[]): number[] {
  if (nums.length <= 1) return nums;

  const mid = Math.floor(nums.length / 2);
  const left = mergeSort(nums.slice(0, mid));
  const right = mergeSort(nums.slice(mid));
  return merge(left, right);
}

function merge(left: number[], right: number[]): number[] {
  const merged: number[] = [];
  let i = 0;
  let j = 0;

  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) merged.push(left[i++]);
    else merged.push(right[j++]);
  }

  return merged.concat(left.slice(i)).concat(right.slice(j));
}

console.log(mergeSort([5, 2, 9, 1, 7]));
```

Expected output: `[1, 2, 5, 7, 9]`.

### Java solution (Java 17+)

```java
import java.util.Arrays;

class Solution {
    static int[] mergeSort(int[] nums) {
        if (nums.length <= 1) return nums;

        int midpoint = nums.length / 2;
        int[] left = mergeSort(Arrays.copyOfRange(nums, 0, midpoint));
        int[] right = mergeSort(Arrays.copyOfRange(nums, midpoint, nums.length));
        return merge(left, right);
    }

    static int[] merge(int[] left, int[] right) {
        int[] merged = new int[left.length + right.length];
        int i = 0, j = 0, k = 0;

        while (i < left.length && j < right.length) {
            if (left[i] <= right[j]) merged[k++] = left[i++];
            else merged[k++] = right[j++];
        }

        while (i < left.length) merged[k++] = left[i++];
        while (j < right.length) merged[k++] = right[j++];
        return merged;
    }

    public static void main(String[] args) {
        int[] nums = {5, 2, 9, 1, 7};
        System.out.println(Arrays.toString(mergeSort(nums)));
    }
}
```

Expected output: `[1, 2, 5, 7, 9]`.

## Problem: Quick sort

**Problem:** Partition an array and recursively sort left and right partitions.

### TypeScript solution

```ts
function quickSort(nums: number[]): number[] {
  if (nums.length <= 1) return nums;

  const pivot = nums[nums.length - 1];
  const left: number[] = [];
  const right: number[] = [];

  for (let i = 0; i < nums.length - 1; i++) {
    if (nums[i] <= pivot) left.push(nums[i]);
    else right.push(nums[i]);
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}

console.log(quickSort([3, 1, 2, 5, 4]));
```

Expected output: `[1, 2, 3, 4, 5]`.

## Complexity and trade-offs

- Merge sort is deterministic O(n log n) time in all cases and stable, but uses O(n) extra space.
- Quick sort is a classic average-case O(n log n); worst-case O(n²) if the pivot choice is poor or input is already sorted and the pivot is always the smallest or largest element.
- Heap sort is O(n log n) worst-case and O(1) extra space, but it is not stable.
- Insertion sort is O(n²) overall but excels when arrays are nearly sorted and the dataset is tiny.
- Counting sort and radix sort are linear or near-linear for bounded integer keys, but they are not general-purpose comparison sorts.

## Common mistakes

- Claiming quick sort is always O(n log n); worst-case O(n²) exists.
- Forgetting that merge sort is stable and uses extra memory.
- Confusing stable and in-place behavior.
- Using counting sort on non-integer or huge key ranges without considering memory blow-up.
- Ignoring large-constraint behavior and assuming the sorted-data pattern is always optimal.

## Interview questions

### Q1: Which sort is best for nearly sorted data?
**Model answer:** Insertion sort is often best because it only moves elements when needed, and the work is close to O(n) when the array is already near-sorted.

### Q2: Why is merge sort often used in interviews?
**Model answer:** It is stable, deterministic O(n log n), and easy to reason about using divide-and-conquer and in-place merge logic.

### Q3: What is the worst-case of quick sort?
**Model answer:** O(n²), which occurs when the pivot repeatedly splits the array into very uneven partitions, such as a sorted list with a poor pivot strategy.

### Q4: Why is counting sort not a general comparison sort?
**Model answer:** It is based on the key range and counts frequencies, so it only works well when the keys are integers in a manageable range.

### Q5: What is stability in sorting?
**Model answer:** A stable sort preserves the relative order of equal elements. This matters for multi-key ordering or when the result needs to preserve insertion order among duplicates.

### Q6: When would you prefer heap sort?
**Model answer:** When you need O(n log n) worst-case time and in-place sorting without the stability requirement, heap sort is a strong option.

### Q7: Why is merge sort good for external sorting?
**Model answer:** Because it naturally streams sorted runs and combines them with predictable cost, which makes it useful for large files that do not fit in memory.

### Q8: How do you choose between sort implementations in practice?
**Model answer:** The decision depends on data size, key distribution, memory constraints, stability needs, and whether the data is already partially ordered.

### Q9: Is quick sort in-place?
**Model answer:** The standard recursive algorithm uses the input array and stack space, so it is in-place with respect to the array content but not necessarily constant stack space in the worst-case recursion depth.

### Q10: What is the difference between a comparison sort and a counting sort?
**Model answer:** Comparison sort decides order by comparing keys; counting sort counts occurrences of keys in a bounded range. The latter is often linear when the domain is small and dense enough.

## Related notes

- [Arrays and hashing](arrays-and-hashing.md)
- [Binary search](binary-search.md)
- [Complexity cheat sheet](complexity-cheat-sheet.md)
- [Greedy algorithms](greedy.md)
