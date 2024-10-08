---
type: leetcode
title: 827. making a large island
tags:
  - dfs
  - hashmap
aliases: 
parents:
  - "[[200-number-of-islands]]"
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-17
---

You are given an `n x n` binary matrix `grid`. You are allowed to change **at most one** `0` to be `1`.

Return _the size of the largest **island** in_ `grid` _after applying this operation_.

An **island** is a 4-directionally connected group of `1`s.

## solution

Instead of brute-forcing each check, we can assign an ID to each island and track their sizes in a hashmap (either modify the matrix or store island membership in a hashmap).

Then, for each 0, check if making it land would add to or link up multiple existing islands.

```python
def largestIsland(self, grid: List[List[int]]) -> int:
	n = len(grid)
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	island_sizes = defaultdict(int)
	island_num = 2
	  
	def dfs(x, y):
		grid[x][y] = island_num
		island_sizes[island_num] += 1
		  
		for dx, dy in dirs:
			nx, ny = x+dx, y+dy
			if 0 <= nx < n and 0 <= ny < n:
				if grid[nx][ny] == 1:
					dfs(nx, ny)

	# sink islands, give unique value, count size
	for i in range(n):
		for j in range(n):
			if grid[i][j] == 1:
				dfs(i, j)
				island_num += 1

	# for each 0, flip and see what islands it would add to/link up
	ans = 0
	for i in range(n):
		for j in range(n):
			if grid[i][j] == 0:
				adjacent_islands = set()
				for dx, dy in dirs:
					ni, nj = i+dx, j+dy
					if 0 <= ni < n and 0 <= nj < n:
						if grid[ni][nj] > 0:
							adjacent_islands.add(grid[ni][nj])
				combined_island_size = 1
				for adj in adjacent_islands:
					combined_island_size += island_sizes[adj]
				ans = max(ans, combined_island_size)
	return ans if ans > 0 else max(island_sizes.values())
```
