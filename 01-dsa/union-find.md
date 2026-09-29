---
title: "Union find"
tags: ["dsa","union-find"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Union find

## Definition

Union-find, also called disjoint set union (DSU), tracks connected components and supports fast union and find operations. It is widely used for connectivity and cycle-detection problems.

## Typical complexity

- Find: O(?(n)) amortized
- Union: O(?(n)) amortized
- Space: O(n)

## Problem 1: Number of connected components

```ts
function countComponents(n: number, edges: number[][]): number {
  const parent = Array.from({ length: n }, (_, i) => i);
  const rank = Array(n).fill(0);

  const find = (x: number): number => {
    if (parent[x] !== x) parent[x] = find(parent[x]);
    return parent[x];
  };

  const union = (a: number, b: number) => {
    const rootA = find(a);
    const rootB = find(b);
    if (rootA === rootB) return;
    if (rank[rootA] < rank[rootB]) {
      parent[rootA] = rootB;
    } else if (rank[rootA] > rank[rootB]) {
      parent[rootB] = rootA;
    } else {
      parent[rootB] = rootA;
      rank[rootA] += 1;
    }
  };

  for (const [a, b] of edges) union(a, b);

  const roots = new Set<number>();
  for (let i = 0; i < n; i++) roots.add(find(i));
  return roots.size;
}
```

## Problem 2: Cycle detection in undirected graph

```ts
function hasCycle(n: number, edges: number[][]): boolean {
  const parent = Array.from({ length: n }, (_, i) => i);

  const find = (x: number): number => {
    if (parent[x] !== x) parent[x] = find(parent[x]);
    return parent[x];
  };

  const union = (a: number, b: number): boolean => {
    const rootA = find(a);
    const rootB = find(b);
    if (rootA === rootB) return false;
    parent[rootA] = rootB;
    return true;
  };

  for (const [a, b] of edges) {
    if (!union(a, b)) return true;
  }

  return false;
}
```

## Problem 3: Accounts merge

```ts
function accountsMerge(accounts: string[][]): string[][] {
  const parent = new Map<string, string>();
  const emailToName = new Map<string, string>();

  const find = (email: string): string => {
    if (!parent.has(email)) parent.set(email, email);
    if (parent.get(email) !== email) parent.set(email, find(parent.get(email)!));
    return parent.get(email)!;
  };

  const union = (a: string, b: string) => {
    const rootA = find(a);
    const rootB = find(b);
    if (rootA !== rootB) parent.set(rootA, rootB);
  };

  for (const account of accounts) {
    const name = account[0];
    const firstEmail = account[1];
    emailToName.set(firstEmail, name);
    for (let i = 1; i < account.length; i++) {
      emailToName.set(account[i], name);
      union(firstEmail, account[i]);
    }
  }

  const groups = new Map<string, Set<string>>();
  for (const email of emailToName.keys()) {
    const root = find(email);
    if (!groups.has(root)) groups.set(root, new Set());
    groups.get(root)!.add(email);
  }

  return Array.from(groups.entries()).map(([root, emails]) => [emailToName.get(root)!, ...Array.from(emails).sort()]);
}
```

## Common mistakes

- Forgetting path compression.
- Not tracking the root for all members.
- Mixing union-find with graph traversal semantics without understanding connected components.

## Related notes

- [BFS / DFS](bfs-dfs.md)
- [Patterns overview](patterns-overview.md)
- [Trie](trie.md)
