---
title: "LeetCode Roadmap: Blind 75 & NeetCode 150"
tags: ["dsa","practice","roadmap"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# LeetCode Roadmap

This roadmap tracks progress through the Blind 75 and NeetCode 150 lists. The focus is on **pattern recognition** rather than quantity.

## Study Strategy
1. **Identify Pattern**: Group problems by the technique they use (e.g., Two Pointers, Sliding Window).
2. **Brute Force $\rightarrow$ Optimal**: Always articulate the $O(n^2)$ solution before implementing the $O(n \log n)$ or $O(n)$ one.
3. **Edge Case Analysis**: Explicitly test for empty inputs, single-element arrays, and large constraints.
4. **Time/Space Complexity**: Document the Big-O for every solution.

## Progress Tracker

| Category | Problem | Pattern | Status | Note |
| :--- | :--- | :--- | :---: | :--- |
| **Arrays & Hashing** | Two Sum | Hash Map | ✅ | |
| | Valid Anagram | Hash Map | ⬜ | |
| | Group Anagrams | Hash Map | ⬜ | |
| | Top K Frequent | Heap/Bucket | ✅ | See `01-dsa/heap.md` |
| | Product of Array Except Self | Prefix Sum | ⬜ | |
| | Longest Consecutive Seq | Hash Set | ⬜ | |
| **Two Pointers** | Valid Palindrome | Two Pointers | ✅ | |
| | 3Sum | Sort + 2P | ⬜ | |
| | Container With Most Water | Two Pointers | ⬜ | |
| **Sliding Window** | Longest Substring w/o Repeat | Window | ✅ | |
| | Longest Repeating Char Replace | Window | ⬜ | |
| | Minimum Window Substring | Window | ✅ | See `01-dsa/sliding-window.md` |
| **Stack** | Valid Parentheses | Stack | ⬜ | |
| | Min Stack | Stack | ⬜ | |
| | Daily Temperatures | Monotonic Stack | ✅ | |
| **Binary Search** | Binary Search | BS | ✅ | |
| | Search in Rotated Sorted Array | BS | ⬜ | |
| | Koko Eating Bananas | BS on Answer | ⬜ | |
| **Linked List** | Reverse Linked List | Iterative/Rec | ⬜ | |
| | Linked List Cycle | Fast/Slow | ✅ | See `01-dsa/linked-lists.md` |
| | Merge K Sorted Lists | Heap | ✅ | See `01-dsa/heap.md` |
| | LRU Cache | DLL + Map | ⬜ | |
| **Trees** | Invert Binary Tree | Recursion | ⬜ | |
| | Max Depth of Binary Tree | DFS | ⬜ | |
| | Binary Tree Level Order | BFS | ✅ | See `01-dsa/bfs-dfs.md` |
| | Validate BST | DFS/Range | ⬜ | |
| **Heap** | Kth Largest in Array | Min Heap | ✅ | See `01-dsa/heap.md` |
| | Find Median from Data Stream | Two Heaps | ⬜ | |
| **Backtracking** | Subsets | Backtrack | ✅ | |
| | Permutations | Backtrack | ✅ | |
| | N-Queens | Backtrack | ✅ | |
| **Graphs** | Number of Islands | BFS/DFS | ✅ | |
| | Course Schedule | Topo Sort | ✅ | See `01-dsa/graph-algorithms.md` |
| | Alien Dictionary | Topo Sort | ⬜ | |
| **DP** | Climbing Stairs | 1D DP | ✅ | |
| | House Robber | 1D DP | ✅ | |
| | Longest Common Subsequence | 2D DP | ✅ | See `01-dsa/knapsack-lcs-lis.md` |
| | Longest Increasing Subsequence | DP/Binary Search | ✅ | See `01-dsa/knapsack-lcs-lis.md` |
| | 0/1 Knapsack | 2D DP | ✅ | See `01-dsa/knapsack-lcs-lis.md` |

## High-Frequency Patterns Summary

- **Two Pointers**: Use when the array is sorted or you need to compare elements from both ends.
- **Sliding Window**: Use for contiguous subarrays/substrings with a specific constraint.
- **Monotonic Stack**: Use when looking for the "next greater" or "next smaller" element.
- **Topological Sort**: Use for dependency resolution in DAGs.
- **DP State Design**: Focus on `dp[i]` meaning. Is it "the max value at index $i$" or "the number of ways to reach $i$"?

## Related notes

- [DSA Patterns Overview](patterns-overview.md)
- [Complexity Cheat Sheet](complexity-cheat-sheet.md)
