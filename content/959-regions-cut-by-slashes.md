---
type: leetcode
title: 959. regions cut by slashes
tags:
  - dfs
  - graph
aliases: 
parents:
  - "[[200-number-of-islands]]"
children: 
supports: 
enemies: 
date: 2024-08-24
updated: 2024-08-24
---

An `n x n` grid is composed of `1 x 1` squares where each `1 x 1` square consists of a `'/'`, `'\'`, or blank space `' '`. These characters divide the square into contiguous regions.

Given the grid `grid` represented as a string array, return _the number of regions_.

Note that backslash characters are escaped, so a `'\'` is represented as `'\\'`.

## solutions

This is quite a challenging medium, and the intuition here can lead you down several roads.

Basically, after we realize that it’s very difficult to convert the abstract solve-by-hand approach of just counting shapes into code, we want to figure out a more systematic approach to handle each cell.

First, we note that each cell is essentially split in either diagonal depending on `/` or `\`. In this way, we can think about each 1x1 cell as containing four triangles that can be disjoint or connected.

### magnification + sinking

With the above intuition, we can decide to represent each cell as 0s and 1s, such that 0s are the lines/borders, and everything else is a 1.

After that, we can just solve the problem exactly like [[200-number-of-islands]].

Note that I originally magnified each cell to a 2x2 grid of 0s and 1s, but that fails on a test case like `["//","/ "]`, as a single diagonal line of an island is not correctly counted with just 4-directional DFS.

```python
def regionsBySlashes(self, grid: List[str]) -> int:
	n = len(grid)
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]

	# construct matrix
	mat = [[1]*(3*n) for _ in range(3*n)]
	for i, row in enumerate(grid):
		for j, char in enumerate(row):
			if char == " ":
				continue
			if char == "/":
				mat[i*3+2][j*3] = 0
				mat[i*3+1][j*3+1] = 0
				mat[i*3][j*3+2] = 0
			else: # \
				mat[i*3][j*3] = 0
				mat[i*3+1][j*3+1] = 0
				mat[i*3+2][j*3+2] = 0

	def sink(x, y):
		mat[x][y] = 0
	  
		for dx, dy in dirs:
			nx, ny = x+dx, y+dy
			if 0 <= nx < len(mat) and 0 <= ny < len(mat):
				if mat[nx][ny] == 1:
					sink(nx, ny)
	  
	ans = 0
	for i in range(len(mat)):
		for j in range(len(mat)):
			if mat[i][j] == 1:
				sink(i, j)
				ans += 1
	return ans
```

### disjoint set union (union find)

I had an inkling that this problem could be a union find, but wasn’t sure how to proceed.

The idea is to consider each of the aforementioned triangles in a cell as a node, and then join them based on several logical conditions.

1. The bottom triangle of a cell will always connect to the top triangle of the cell below it, and likewise for left and right triangles of adjacent cells.
2. If a cell contains no divider, we can connect all of them. If a cell contains a divider, logically connect up the two connections required.

Use union find to make all of these connections. After iterating through all of the cells, just return the number of disjoint components.

```python
def regionsBySlashes(self, grid: List[str]) -> int:
	n = len(grid)
	# triangle order: top, right, bottom, left
	parents = [x for x in range(n*n*4)]
	sizes = [1]*(n*n*4)
	  
	# index of triangle = i*n*4 + j*4 + triangle offset
	# (top=0, right=1, ...)
	def _get_triangle_idx(i, j, pos):
		dirs = {
			"top": 0,
			"right": 1,
			"bottom": 2,
			"left": 3
		}
		base = i*n*4 + j*4
		return base + dirs[pos]
	  
	def find(node):
		if node != parents[node]:
			parents[node] = find(parents[node])
		return parents[node]

	def union(u, v):
		pu, pv = find(u), find(v)
	  
		if pu == pv:
			return
	  
		# pu is bigger, make it the root
		if sizes[pv] > sizes[pu]:
			pu, pv = pv, pu
	  
		parents[pv] = pu
		sizes[pu] += sizes[pv]
	  
	for i in range(n):
		for j in range(n):
			# connect left triangle to previous right
			if j > 0:
				union(
					_get_triangle_idx(i, j, "left"),
					_get_triangle_idx(i, j-1, "right")
				)
	  
			# connect top triangle to previous bottom
			if i > 0:
				union(
					_get_triangle_idx(i, j, "top"),
					_get_triangle_idx(i-1, j, "bottom")
				)
	  
			# handle divider
			if grid[i][j] == " ":
				union(
					_get_triangle_idx(i, j, "top"),
					_get_triangle_idx(i, j, "right")
				)
				union(
					_get_triangle_idx(i, j, "bottom"),
					_get_triangle_idx(i, j, "right")
				)
				union(
					_get_triangle_idx(i, j, "bottom"),
					_get_triangle_idx(i, j, "left")
				)
				union(
					_get_triangle_idx(i, j, "top"),
					_get_triangle_idx(i, j, "left")
				)
			elif grid[i][j] == "/":
				union(
					_get_triangle_idx(i, j, "top"),
					_get_triangle_idx(i, j, "left")
				)
				union(
					_get_triangle_idx(i, j, "bottom"),
					_get_triangle_idx(i, j, "right")
				)
			else: # \
				union(
					_get_triangle_idx(i, j, "top"),
					_get_triangle_idx(i, j, "right")
				)
				union(
					_get_triangle_idx(i, j, "bottom"),
					_get_triangle_idx(i, j, "left")
				)
	  
	parents = [find(p) for p in parents]
	return len(set(parents))
```
