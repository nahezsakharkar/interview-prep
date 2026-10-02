---
title: "Binary Search Tree"
tags: ["dsa","tree","bst"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Binary Search Tree

## Definition

A binary search tree (BST) is a binary tree where every node satisfies the invariant: every value in the left subtree is smaller than the node, and every value in the right subtree is greater than the node. This allows efficient ordered lookup.

## When to use

- Search, insertion, and deletion in sorted data when the tree remains reasonably balanced.
- Ordered iteration via in-order traversal.
- Range queries over a sorted set.
- Building balanced or self-adjusting tree structures such as AVL or red-black trees for stricter guarantees.

## Key properties

- In-order traversal visits values in sorted order.
- Search, insert, and delete are average O(log n) when the tree stays balanced.
- Worst-case height is O(n) for a skewed tree; balancing strategies prevent this.
- Duplicate handling must be defined explicitly (e.g. insert to the left, right, or reject duplicates).

## Complexity

| Operation | Best | Average | Worst | Extra space |
| --- | --- | --- | --- | --- |
| Search | O(1) | O(log n) | O(n) | O(1) |
| Insert | O(1) | O(log n) | O(n) | O(1) for iterative; O(h) recursion stack |
| Delete | O(1) | O(log n) | O(n) | O(1) for iterative; O(h) recursion stack |
| In-order traversal | O(n) | O(n) | O(n) | O(h) recursive/stack |

## Problem: Search and insert

**Problem:** Given a BST and a target value, determine if it exists. Then insert it if missing.

**Pattern:** BST invariant plus recursive or iterative descent.

### TypeScript solution

```ts
class TreeNode {
  val: number;
  left: TreeNode | null;
  right: TreeNode | null;

  constructor(val: number) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function searchBST(root: TreeNode | null, target: number): TreeNode | null {
  let current = root;
  while (current !== null) {
    if (target === current.val) return current;
    if (target < current.val) current = current.left;
    else current = current.right;
  }
  return null;
}

function insertBST(root: TreeNode | null, value: number): TreeNode {
  if (root === null) return new TreeNode(value);

  if (value < root.val) root.left = insertBST(root.left, value);
  else if (value > root.val) root.right = insertBST(root.right, value);

  return root;
}

const root = new TreeNode(5);
insertBST(root, 3);
insertBST(root, 7);
console.log(searchBST(root, 7)?.val);
```

Expected output: `7`.

### Java solution (Java 17+)

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int val) {
        this.val = val;
    }
}

class Solution {
    static TreeNode searchBST(TreeNode root, int target) {
        TreeNode current = root;
        while (current != null) {
            if (target == current.val) return current;
            if (target < current.val) current = current.left;
            else current = current.right;
        }
        return null;
    }

    static TreeNode insertBST(TreeNode root, int value) {
        if (root == null) return new TreeNode(value);
        if (value < root.val) root.left = insertBST(root.left, value);
        else if (value > root.val) root.right = insertBST(root.right, value);
        return root;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(5);
        insertBST(root, 3);
        insertBST(root, 7);
        System.out.println(searchBST(root, 7).val);
    }
}
```

Expected output: `7`.

## Problem: Delete a node

**Problem:** Remove a target value from a BST while preserving the BST invariant.

### Approach

There are three common cases:

1. Node has no children: remove it directly.
2. Node has one child: replace it with that child.
3. Node has two children: replace the node with its in-order successor or predecessor, then delete that successor/predecessor recursively.

### TypeScript solution

```ts
function deleteNode(root: TreeNode | null, key: number): TreeNode | null {
  if (root === null) return null;

  if (key < root.val) {
    root.left = deleteNode(root.left, key);
    return root;
  }
  if (key > root.val) {
    root.right = deleteNode(root.right, key);
    return root;
  }

  if (root.left === null) return root.right;
  if (root.right === null) return root.left;

  const successor = findMin(root.right);
  root.val = successor.val;
  root.right = deleteNode(root.right, successor.val);
  return root;
}

function findMin(node: TreeNode): TreeNode {
  while (node.left !== null) node = node.left;
  return node;
}
```

### Complexity

- Delete in a balanced BST: O(log n) average, O(n) worst.
- The combined cost for successor lookup and recursive delete remains proportional to tree height.

## Dry run for delete

For a tree with root `10` and right subtree containing `15`, deleting `10` by in-order successor uses `15` as the replacement value, then deletes the original `15` node from the right subtree. This preserves the BST rule that all right-subtree values are greater than the replacement value.

## Common mistakes

- Confusing the BST invariant with a heap invariant; heaps are about parent-child ordering, not sorted-order traversal.
- Forgetting to handle the two-child deletion case correctly.
- Assuming the tree stays balanced without explicit balancing strategies.
- Allowing duplicate definitions to violate the invariant or produce ambiguous semantics.
- Using recursion without checking for null children in deep skewed trees.

## Interview questions

### Q1: What property makes a BST useful?
**Model answer:** The in-order traversal gives sorted values, and left/right bounds let us prune the search space quickly.

### Q2: What is the average height of a BST?
**Model answer:** In a roughly balanced BST, it is O(log n). In an unbalanced tree, it can degrade to O(n), effectively turning operations into linear scans.

### Q3: Why is in-order traversal sorted?
**Model answer:** Every left subtree is smaller than the current node, and every right subtree is larger, so visiting left → current → right yields ascending order.

### Q4: How do you delete a node with two children?
**Model answer:** Replace it with its in-order successor or predecessor, then delete that successor/predecessor from the original subtree.

### Q5: Why do balanced BSTs exist?
**Model answer:** A plain BST can become skewed under ordered inserts; AVL, red-black, and treap trees maintain height bounds that keep operations near O(log n).

### Q6: What is the difference between a BST and a binary heap?
**Model answer:** BST enforces sorted ordering between subtrees; heap enforces parent-child ordering but not sorted in-order traversal. A heap's root is the minimum or maximum, but a BST root is not necessarily the smallest or largest value.

### Q7: Which traversal gives sorted order?
**Model answer:** In-order traversal. Pre-order and post-order are useful for structural tasks and expression tree evaluation, not sorted order.

### Q8: What if duplicates are allowed?
**Model answer:** Define a consistent convention such as placing duplicates in the left subtree, the right subtree, or rejecting duplicates. The choice should be explicit because it changes search and delete behavior.

### Q9: What is the worst-case complexity for search in a BST?
**Model answer:** O(n) if the tree is skewed, because the search path can become a linked list.

### Q10: When would you not choose a BST?
**Model answer:** When you need faster average-case guarantees or better cache locality for large datasets, a balanced tree, hash table, or specialized index may be more appropriate.

## Related notes

- [Tree traversal](tree-traversal.md)
- [BFS / DFS](bfs-dfs.md)
- [Heap](heap.md)
- [Complexity cheat sheet](complexity-cheat-sheet.md)
