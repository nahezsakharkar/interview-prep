---
title: "Trie"
tags: ["dsa","trie"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Trie

## Definition

A trie is a tree-like structure used for efficient prefix-based lookup. It is especially useful in dictionaries, autocomplete, and prefix matching tasks.

## Typical complexity

- Insert: O(L)
- Search: O(L)
- Prefix check: O(L)
- Space: O(total characters)

## Problem 1: Implement trie

```ts
class TrieNode {
  children: Map<string, TrieNode>;
  isEnd: boolean;

  constructor() {
    this.children = new Map();
    this.isEnd = false;
  }
}

class Trie {
  root: TrieNode;

  constructor() {
    this.root = new TrieNode();
  }

  insert(word: string): void {
    let node = this.root;
    for (const ch of word) {
      if (!node.children.has(ch)) node.children.set(ch, new TrieNode());
      node = node.children.get(ch)!;
    }
    node.isEnd = true;
  }

  search(word: string): boolean {
    let node = this.root;
    for (const ch of word) {
      if (!node.children.has(ch)) return false;
      node = node.children.get(ch)!;
    }
    return node.isEnd;
  }
}
```

## Problem 2: Longest common prefix

```ts
function longestCommonPrefix(words: string[]): string {
  if (!words.length) return '';

  let prefix = words[0];
  for (let i = 1; i < words.length; i++) {
    while (!words[i].startsWith(prefix)) {
      prefix = prefix.slice(0, -1);
      if (!prefix) return '';
    }
  }

  return prefix;
}
```

## Problem 3: Word search II

```ts
function findWords(board: string[][], words: string[]): string[] {
  const trie = new Map<string, any>();
  for (const word of words) {
    let node = trie;
    for (const ch of word) {
      if (!node[ch]) node[ch] = {};
      node = node[ch];
    }
    node.isEnd = true;
  }

  const rows = board.length;
  const cols = board[0].length;
  const result = new Set<string>();
  const visited = new Set<string>();

  const dfs = (r: number, c: number, node: any, word: string) => {
    if (node.isEnd) result.add(word);
    if (r < 0 || c < 0 || r >= rows || c >= cols) return;
    const key = `${r},${c}`;
    if (visited.has(key)) return;
    visited.add(key);

    const ch = board[r][c];
    const next = node[ch];
    if (!next) {
      visited.delete(key);
      return;
    }

    const directions = [[1,0],[-1,0],[0,1],[0,-1]];
    for (const [dr, dc] of directions) {
      dfs(r + dr, c + dc, next, word + ch);
    }

    visited.delete(key);
  };

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      dfs(r, c, trie, '');
    }
  }

  return Array.from(result);
}
```

## Common mistakes

- Using a map or array without accounting for the prefix tree structure.
- Not distinguishing between a valid word and a prefix node.
- Not pruning correctly during word-search traversal.

## Related notes

- [BFS / DFS](bfs-dfs.md)
- [Backtracking](backtracking.md)
- [Patterns overview](patterns-overview.md)
