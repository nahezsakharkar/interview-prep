---
title: "Bit Manipulation"
tags: ["dsa","bitwise","binary"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Bit Manipulation

## Definition

Bit manipulation works directly on the binary representation of integers. It is useful for performance-sensitive tasks, compact flags, and set membership when the domain is small and fixed-size.

## Core operations

| Operation | Meaning | Example |
| --- | --- | --- |
| `x & (1 << i)` | Check if bit `i` is set | `mask & 1` |
| `x | (1 << i)` | Set bit `i` | turn on a flag |
| `x & ~(1 << i)` | Clear bit `i` | turn off a flag |
| `x ^ (1 << i)` | Toggle bit `i` | flip a flag |
| `x >> 1` | Arithmetic right shift | divide by 2 |
| `x << 1` | Left shift | multiply by 2 |
| `x & (x - 1)` | Clear the lowest set bit | count trailing zeros |

## Why it matters

- It gives compact state tracking with O(1) per operation.
- It is often used in subset enumeration, bitmasks, and dense boolean flags.
- It supports high-performance numeric logic in algorithms and hardware-adjacent code.

## Complexity reference

| Operation | Cost |
| --- | --- |
| Single bit check / set / clear | O(1) |
| Iterate over bits in a number | O(log n) or O(b) for `b` bits |
| Subset enumeration over `n` items | O(2^n) total states |
| Space for a bitmask | O(1) if stored in an integer, O(n) for array-backed flags |

## Problem: Count set bits

**Problem:** Return the number of `1` bits in a non-negative integer.

**Pattern:** Repeatedly clear the lowest set bit.

### TypeScript solution

```ts
function countSetBits(n: number): number {
  let count = 0;
  while (n > 0) {
    n &= n - 1;
    count++;
  }
  return count;
}

console.log(countSetBits(13));
```

Expected output: `3` because `13` is binary `1101`.

### Java solution (Java 17+)

```java
class Solution {
    static int countSetBits(int n) {
        int count = 0;
        while (n > 0) {
            n &= (n - 1);
            count++;
        }
        return count;
    }

    public static void main(String[] args) {
        System.out.println(countSetBits(13));
    }
}
```

Expected output: `3`.

## Problem: Check if a number is a power of two

**Pattern:** `n > 0 && (n & (n - 1)) === 0`.

### TypeScript solution

```ts
function isPowerOfTwo(n: number): boolean {
  return n > 0 && (n & (n - 1)) === 0;
}

console.log(isPowerOfTwo(8));
console.log(isPowerOfTwo(10));
```

Expected output: `true` and `false`.

## Common mistakes

- Forgetting that bit operations work on signed integers, which may have sign-extension and negative value behavior.
- Using the wrong mask when clearing or toggling a bit.
- Assuming bit operations are always faster than arithmetic; clarity and correctness matter most unless profiling demands micro-optimization.
- Confusing left/right shift semantics; especially with negative values and JavaScript's bitwise conversion behavior.
- Forgetting that `x & (x - 1)` only removes the lowest set bit and does not count all ones at once.

## Interview questions

### Q1: What does `x & (x - 1)` do?
**Model answer:** It clears the lowest set bit of `x` while preserving higher bits. This is the basis for bit-count loops and power-of-two checks.

### Q2: How do you check if bit `i` is set?
**Model answer:** Use `mask & (1 << i)`. If the result is non-zero, the bit is set.

### Q3: How do you set bit `i`?
**Model answer:** Use `mask | (1 << i)`.

### Q4: How do you clear bit `i`?
**Model answer:** Use `mask & ~(1 << i)`.

### Q5: How do you toggle bit `i`?
**Model answer:** Use `mask ^ (1 << i)`.

### Q6: Why is power-of-two check efficient?
**Model answer:** A positive power-of-two number has exactly one set bit, so `n & (n - 1)` becomes zero after removing that single bit.

### Q7: What is a bitmask?
**Model answer:** A compact set representation where each bit corresponds to a choice or property. Bitmasks let you represent many boolean flags in one integer.

### Q8: Can bit manipulation be used for subsets?
**Model answer:** Yes. If there are `n` items, each subset can be represented as an integer mask of length `n` bits, allowing enumeration in O(2^n) states.

### Q9: What is the difference between arithmetic and logical right shifts?
**Model answer:** In Java, `>>` is arithmetic for signed values; `>>>` is logical and preserves zero-fill. JavaScript bitwise operators operate on 32-bit signed integers, which matters for larger values.

### Q10: When should you avoid bit manipulation?
**Model answer:** When clarity and maintainability matter more than a micro-optimization, or when the domain value range is large, sparse, or not naturally represented by fixed-size bits.

## Related notes

- [Sorting algorithms](sorting.md)
- [Binary search tree](binary-search-tree.md)
- [Complexity cheat sheet](complexity-cheat-sheet.md)
- [Greedy algorithms](greedy.md)
