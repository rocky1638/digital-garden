---
type: leetcode
title: 1079. letter tile possibilities
tags:
  - backtracking
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-04-22
---

You have `n`  `tiles`, where each tile has one letter `tiles[i]` printed on it.

Return _the number of possible non-empty sequences of letters_ you can make using the letters printed on those `tiles`.

## solution

We use a depth-first search to enumerate all the possibilities. To avoid duplicates and infinite loops, we use a `used` set to keep track of which indices we’ve already used at each step of the DFS.

```python
def numTilePossibilities(self, tiles: str) -> int:
	used = set()
	sequences = set()

	def dfs(acc):
		if len(acc) > len(tiles):
			return if len(acc) > 0 and acc not in sequences:
			sequences.add(acc)

		for i in range(len(tiles)):
			if i not in used:
				used.add(i)
				dfs(acc+tiles[i])
				used.remove(i)
				
	dfs("")
	return len(sequences)
```
