---
type: leetcode
title: "1042. flower planting with no adjacent"
tags:
  - graph
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-19
---

You have `n` gardens, labeled from `1` to `n`, and an array `paths` where `paths[i] = [xi, yi]` describes a bidirectional path between garden `xi` to garden `yi`. In each garden, you want to plant one of 4 types of flowers.

All gardens have **at most 3** paths coming into or leaving it.

Your task is to choose a flower type for each garden such that, for any two gardens connected by a path, they have different types of flowers.

Return _**any** such a choice as an array_ `answer`_, where_ `answer[i]` _is the type of flower planted in the_ `(i+1)th` _garden. The flower types are denoted_ `1`_,_ `2`_,_ `3`_, or_ `4`_. It is guaranteed an answer exists._

## solution

This is a standard **graph coloring** problem that asks us to generate a valid coloring for a graph.

The procedure is as follows:

1. Iterate through the nodes from 1 to `n`. We do this recursively to allow us to backtrack.
2. For the current node, we pick the next available color that works (that doesn’t conflict with neighboring nodes).
	- We can do this because if the neighbors have colors 1 and 2, and we can pick from 3 and 4, it doesn’t matter which one we pick.
3. Move onto the next node.
4. If our path doesn’t yield a valid solution, we won’t reach line 26, and will essentially backtrack to the previous node, picking the next valid color.

```python
def gardenNoAdj(self, n: int, paths: List[List[int]]) -> List[int]:
	g = defaultdict(list)
	for u1, u2 in paths:
		g[u1].append(u2)
		g[u2].append(u1)
	
	colors = [0]*n
 
	def is_valid(color, node):
		nonlocal colors
		for neighbor in g[node]:
			if colors[neighbor-1] == color:
				return False
		return True
	
	def recurse(node):
		nonlocal colors
		if node > n:
			return colors
	
		for color in range(1, 5):
			if is_valid(color, node):
				prev = colors[node-1]
				colors[node-1] = color
				# greedily pick first working color
				return recurse(node+1)
	
	return recurse(1)
```
