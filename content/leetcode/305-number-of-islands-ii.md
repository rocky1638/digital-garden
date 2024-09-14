---
type: leetcode
title: 305. number of islands ii
tags:
  - graph
  - union-find
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-07
updated: 2024-08-26
---

You are given an empty 2D binary grid `grid` of size `m x n`. The grid represents a map where `0`'s represent water and `1`'s represent land. Initially, all the cells of `grid` are water cells (i.e., all the cells are `0`'s).

We may perform an add land operation which turns the water at position into a land. You are given an array `positions` where `positions[i] = [ri, ci]` is the position `(ri, ci)` at which we should operate the `ith` operation.

Return _an array of integers_ `answer` _where_ `answer[i]` _is the number of islands after turning the cell_ `(ri, ci)` _into a land_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## solution

The intuition to use [[union-find]] here is pretty obvious, but the difficulty is wrapping your head around the details of how it works.

A couple of points to note:

- Instead of using a list to store roots and sizes, use dictionaries, keyed by tuples of `(x, y)`.
- We initially start with no nodes, and no sizes.
- When we add a node, it starts out being its own parent, with a size of 1.
	- We then check the 4 “edges”, running `union` on the neighboring node if it exists.

My main hiccup was trying to figure out what would happen if a new node caused two other components to now all become connected. How do we know which component this new node will choose to join?

After some thought, I realized that we `union` each edge in sequence. That means that we first connect the node to component 1. Then, now that the node is a part of component 1, it is unioned with component 2, as normal.

```python
def numIslands2(self, m: int, n: int, positions: List[List[int]]) -> List[int]:
	parents = defaultdict()
	sizes = defaultdict(int)
	dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]]
	components = 0
	  
	def union(coord1, coord2):
		nonlocal components
	  
		p1, p2 = find(coord1), find(coord2)
	  
		if p1 == p2:
			return
	  
		# make p1 always smaller
		if sizes[p1] > sizes[p2]:
			p1, p2 = p2, p1
	  
		parents[p1] = p2
		sizes[p2] += sizes[p1]
		components -= 1
	  
	def find(coord):
		if coord != parents[coord]:
			parents[coord] = find(parents[coord])
		return parents[coord]
	  
	ans = []
	for x, y in positions:
		coord = (x, y)

		# duplicate operation
		if sizes[coord] > 0:
			ans.append(components)
			continue

		sizes[coord] = 1
		parents[coord] = coord
		components += 1
		  
		for dx, dy in dirs:
			nx, ny = x+dx, y+dy
			if 0 <= nx < m and 0 <= ny < n:
				if sizes[(nx, ny)] > 0:
					union((x,y), (nx, ny))
		ans.append(components)
	return ans
```
