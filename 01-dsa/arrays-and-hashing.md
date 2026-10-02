---
title: "Arrays and Hashing"
tags: ["dsa","arrays","hashing"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Arrays and Hashing

## Definition

Arrays store indexed sequences; hash maps and sets store key-based associations or membership. Together they support common patterns such as counting, deduplication, lookup, grouping, and prefix aggregation.

## When to use

- Use an array when order/index access matters or the input is a sequence.
- Use a map when a value must be associated with a key, such as value → index or item → count.
- Use a set when only membership/uniqueness is needed.
- Use a frequency map for anagrams, counts, and repeated-element questions.
- Use prefix sums when many range-sum queries or cumulative constraints appear.

## How it works

An array provides direct indexed access. A hash table hashes a key to a bucket and resolves collisions by its implementation's collision strategy. Interview complexity usually treats hash operations as average O(1), but collisions and resizing affect worst-case behavior.

## Complexity reference

| Operation | Best | Average / expected | Worst | Extra space |
| --- | --- | --- | --- | --- |
| Array index read/write | O(1) | O(1) | O(1) | O(1) |
| Linear search in array | O(1) | O(n) | O(n) | O(1) |
| Hash map get/set | O(1) | O(1) expected | O(n) in a simple collision model; implementation-dependent | O(n) stored entries |
| Set membership/add | O(1) | O(1) expected | O(n) in a simple collision model; implementation-dependent | O(n) stored entries |
| Sort array | Depends on algorithm | Common comparison sorts O(n log n) | Often O(n log n), algorithm-dependent | Algorithm-dependent |

Distinguish the auxiliary space of one operation from the storage of the whole map/set. For a particular language/runtime, verify implementation guarantees rather than assuming every hash table has identical worst-case bounds.

## Problem: Two Sum

**Problem:** Given an integer array and target, return two distinct indices whose values sum to the target, or an empty result if no pair exists.

**Pattern:** Array scan + hash map (complement lookup).

### Approach

For each value `x`, look for `target - x` among values already seen. If present, return its prior index and the current index; otherwise store `x` and its index. Looking up before inserting prevents using one array element twice.

### Brute force vs optimal

| Approach | Idea | Time | Extra space | Trade-off |
| --- | --- | --- | --- | --- |
| Brute force | Check every pair | Best O(1), average/worst O(n²) | O(1) | Simple; no hash assumptions |
| Hash map | Store prior value → index | Best O(1), average O(n), worst O(n²) under a simple pathological collision model | O(n) | Faster expected lookup, additional memory |

### TypeScript solution

```ts
function twoSum(nums: number[], target: number): number[] {
  const indexByValue = new Map<number, number>();

  for (let index = 0; index < nums.length; index++) {
    const value = nums[index];
    const complement = target - value;
    const priorIndex = indexByValue.get(complement);

    if (priorIndex !== undefined) {
      return [priorIndex, index];
    }
    indexByValue.set(value, index);
  }

  return [];
}

console.log(twoSum([2, 7, 11, 15], 9));
```

### Java solution (Java 17+)

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> indexByValue = new HashMap<>();

        for (int index = 0; index < nums.length; index++) {
            int value = nums[index];
            int complement = target - value;
            Integer priorIndex = indexByValue.get(complement);

            if (priorIndex != null) {
                return new int[] { priorIndex, index };
            }
            indexByValue.put(value, index);
        }

        return new int[0];
    }
}
```

Expected result for `[2, 7, 11, 15]`, target `9`: indices `[0, 1]`.

### Dry run

| Index | Value | Complement | Previously seen? | Action |
| ---: | ---: | ---: | --- | --- |
| 0 | 2 | 7 | No | Store `2 → 0` |
| 1 | 7 | 2 | Yes, at index 0 | Return `[0, 1]` |

### Edge cases

- Empty or one-element array: return no pair.
- Duplicate values: `[3, 3]`, target `6` returns distinct indices.
- Negative values and zero are valid.
- If multiple pairs exist, this implementation returns the first found in scan order; confirm whether any valid answer is acceptable.
- Integer overflow behavior differs between Java `int` and JavaScript `number`; constrain inputs or use a wider representation if required.

## Additional pattern: frequency counting

For a lowercase English-letter anagram check, count each character in one string and subtract counts in the other. This is O(n) time and O(1) extra space relative to the fixed alphabet size; for a general Unicode alphabet, a map may require O(k) space for $k$ distinct code points. Clarify whether comparison is by UTF-16 code unit, code point, case, and normalization.

## Complexity and trade-offs

- Two Sum's hash-map solution scans the array once: O(n) expected time, O(n) extra space. Best case can return on the second scanned element; worst-case lookup behavior depends on the hash implementation and key distribution.
- A sorted-array/two-pointer solution uses O(1) extra space but requires sorting first (O(n log n)) or already-sorted input, and sorting may change original index tracking.
- Prefix sums speed repeated range sums after O(n) preprocessing, using O(n) additional space; mutable arrays require update strategies such as Fenwick/segment trees.

## Common mistakes

- Inserting the current value before checking its complement, which can reuse the same element.
- Assuming hash operations are worst-case O(1) in every implementation.
- Reporting map storage as the extra space of each individual lookup.
- Sorting input when original indices/order must be preserved without tracking indices.
- Ignoring duplicate values, empty input, or numeric overflow constraints.

## Interview questions

### Q1: Why is the hash-map Two Sum solution expected O(n)?
**Model answer:** It scans each element once and performs expected constant-time map lookup/insertion per element, so expected total time is O(n), with O(n) storage.

### Q2: Why check the complement before inserting the current value?
**Model answer:** It ensures the matching value came from an earlier, distinct index. Inserting first can allow an element to pair with itself when twice its value equals the target.

### Q3: What is the worst-case complexity of a hash lookup?
**Model answer:** It depends on the implementation and collision behavior. In a simple chained-hash model, many colliding keys can make lookup O(n); runtime-specific implementations may add mitigations, so state assumptions.

### Q4: When is a set better than a map?
**Model answer:** Use a set when only membership or uniqueness matters. Use a map when each key needs associated data such as a frequency, index, or accumulated value.

### Q5: How do you check whether two strings are anagrams?
**Model answer:** Define normalization and character semantics first, then compare frequency counts. For a fixed small alphabet, an array of counts gives O(n) time and O(1) alphabet-sized space; otherwise use a map with O(k) space.

### Q6: When can sorting replace hashing?
**Model answer:** Sorting can simplify duplicate/pair/grouping logic and avoid hash assumptions, but costs O(n log n), may mutate order, and can require preserving original indices.

### Q7: What is a prefix sum?
**Model answer:** It stores cumulative sums so a range sum can be computed by subtracting two prefix values. It gives O(n) preprocessing and O(1) range queries, with O(n) space.

### Q8: How do you handle repeated values in Two Sum?
**Model answer:** Store an index for prior values and check before insertion. For `[x, x]` and target `2x`, the second `x` finds the first index and returns two distinct positions.

### Q9: What does “expected O(1)” mean for a hash map?
**Model answer:** It is an average-case/expected bound under assumptions about hashing and key distribution, not a universal worst-case guarantee.

### Q10: What constraints can change your solution?
**Model answer:** Input ordering, need for original indices, duplicate rules, numeric range, memory limits, and whether the alphabet/key domain is bounded can change the best approach.

## Related notes

- [Patterns overview](patterns-overview.md)
- [Two pointers](two-pointers.md)
- [Sliding window](sliding-window.md)
- [Complexity cheat sheet](complexity-cheat-sheet.md)
