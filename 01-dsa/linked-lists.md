---
title: "Linked Lists"
tags: ["dsa","linked-lists"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Linked Lists

## Definition

A linked list is a sequence of nodes where each node stores a value and one or more links to other nodes. A singly linked list supports forward traversal; a doubly linked list also stores a previous link.

## When to use

- Frequent insertion/removal when the relevant node/predecessor is already known.
- Pointer-manipulation problems such as reverse, merge, cycle detection, or remove-kth-from-end.
- Avoid assuming linked lists are faster than arrays for arbitrary lookup; reaching index $i$ requires traversal.

## How it works

A singly linked node points to the next node or `null`. The `head` references the first node. To mutate links safely, retain the next pointer before overwriting the current node's link. Dummy/sentinel nodes can simplify edge cases at the head.

## Operation complexity

| Operation | Best | Average | Worst | Extra space |
| --- | --- | --- | --- | --- |
| Access index $i$ | O(1) when $i=0$ | O(n) | O(n) | O(1) |
| Search by value | O(1) if first node matches | O(n) | O(n) | O(1) |
| Insert after known node | O(1) | O(1) | O(1) | O(1) |
| Insert at head | O(1) | O(1) | O(1) | O(1) |
| Append without tail pointer | O(1) for empty list | O(n) | O(n) | O(1) |

## Problem: Reverse a singly linked list

**Problem:** Given the head of a singly linked list, reverse its links in place and return the new head.

**Pattern:** Pointer manipulation; maintain previous, current, and next pointers.

### Approach

At each node, save its original `next`, point it back to `previous`, then advance both pointers. When `current` reaches `null`, `previous` is the new head.

### Brute force vs optimal

| Approach | Idea | Time | Extra space | Trade-off |
| --- | --- | --- | --- | --- |
| Copy values | Traverse into an array, then build a reversed list | O(n) | O(n) | Simpler pointer reasoning but allocates nodes/storage and does not reverse the original links in place |
| Iterative pointer reversal | Redirect each `next` link once | Best O(1) for empty list; average/worst O(n) | O(1) | In-place; requires careful pointer order |
| Recursive reversal | Recurse to the end, then reverse links while unwinding | O(n) | O(n) call stack | Concise but can overflow stack on long lists |

### TypeScript solution

```ts
class ListNode {
  val: number;
  next: ListNode | null;

  constructor(val: number, next: ListNode | null = null) {
    this.val = val;
    this.next = next;
  }
}

function reverseList(head: ListNode | null): ListNode | null {
  let previous: ListNode | null = null;
  let current = head;

  while (current !== null) {
    const next = current.next;
    current.next = previous;
    previous = current;
    current = next;
  }

  return previous;
}

function toArray(head: ListNode | null): number[] {
  const values: number[] = [];
  for (let node = head; node !== null; node = node.next) values.push(node.val);
  return values;
}

const head = new ListNode(1, new ListNode(2, new ListNode(3)));
console.log(toArray(reverseList(head)));
```

Expected output: `[3, 2, 1]`.

### Java solution (Java 17+)

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }

    ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}

class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode previous = null;
        ListNode current = head;

        while (current != null) {
            ListNode next = current.next;
            current.next = previous;
            previous = current;
            current = next;
        }

        return previous;
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1, new ListNode(2, new ListNode(3)));
        ListNode reversed = new Solution().reverseList(head);
        for (ListNode node = reversed; node != null; node = node.next) {
            System.out.print(node.val + (node.next == null ? "" : " "));
        }
    }
}
```

Expected output: `3 2 1`.

### Dry run

For `1 → 2 → 3 → null`:

| Iteration | `previous` | `current` | Saved `next` | Link after update |
| ---: | --- | --- | --- | --- |
| Start | `null` | `1` | — | unchanged |
| 1 | `1` | `2` | `2` | `1 → null` |
| 2 | `2` | `3` | `3` | `2 → 1` |
| 3 | `3` | `null` | `null` | `3 → 2` |

Return `previous`, which is node `3`.

## Edge cases

- Empty list returns `null`.
- One node returns the same node.
- Two nodes reverse their single link.
- Preserve the saved next node before changing `current.next` or the remainder becomes unreachable.
- Cyclic input is outside this function's precondition; detect cycles separately if input may be cyclic.

## Complexity / trade-offs

Iterative reversal visits each of $n$ nodes once: best O(1) for an empty list, average/worst O(n) time, and O(1) extra space. It mutates the input list. Recursive reversal uses O(n) call-stack space. Unlike arrays, lists provide O(1) insertion after a known node but O(n) index access and poor cache locality in typical implementations.

## Common mistakes

- Updating `current.next` before saving the original next pointer.
- Returning the old head instead of the new head (`previous`).
- Forgetting the empty and single-node cases.
- Losing a sublist by advancing pointers in the wrong order.
- Claiming arbitrary insertion is O(1) when finding the insertion point itself requires O(n).
- Applying the algorithm to a cyclic list without first handling the cycle.

## Interview questions

### Q1: Why must you save `current.next` before reversing the link?
**Model answer:** Reassigning `current.next` destroys the only forward reference to the unreversed suffix. Saving it first lets the traversal continue.

### Q2: What does `previous` represent at loop exit?
**Model answer:** It points to the last processed node, which is the new head after every original link has been reversed.

### Q3: What are the time and space complexities of iterative reversal?
**Model answer:** It visits each node once, so O(n) worst-case time, and uses a fixed number of pointers, so O(1) auxiliary space. Empty input returns in O(1).

### Q4: Why is linked-list index access O(n)?
**Model answer:** Nodes are reached by following links from the head; there is no direct address calculation for an arbitrary index as in an array.

### Q5: When is insertion into a linked list O(1)?
**Model answer:** When the insertion location or predecessor node is already known. Searching for a location by index/value still costs O(n).

### Q6: How do you detect a cycle in a singly linked list?
**Model answer:** Floyd's tortoise-and-hare algorithm advances one pointer by one step and another by two. If they meet, a cycle exists; otherwise the fast pointer reaches `null`.

### Q7: What is a dummy node useful for?
**Model answer:** It provides a stable predecessor before the original head, simplifying operations that may remove or replace the head.

### Q8: Compare singly and doubly linked lists.
**Model answer:** A doubly linked list supports backward traversal and O(1) removal when a node reference is known, but each node uses more memory and both links must remain consistent.

### Q9: Why can recursion be risky for list reversal?
**Model answer:** Recursion uses O(n) call-stack space and may exceed runtime stack limits for a sufficiently long list; iteration uses constant auxiliary space.

### Q10: Does reversing the list allocate new nodes?
**Model answer:** This iterative method reuses and mutates the existing nodes, allocating only a fixed number of local references.

## Related notes

- [Arrays and hashing](arrays-and-hashing.md)
- [Tree traversal](tree-traversal.md)
- [BFS / DFS](bfs-dfs.md)
- [DSA problem template](../templates/dsa-problem.md)
