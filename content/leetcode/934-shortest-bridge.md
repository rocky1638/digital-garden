---
type: leetcode
title: 934. shortest bridge
tags:
  - dfs
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-17
updated: 2024-08-17
---

You are given an `n x n` binary matrix `grid` where `1` represents land and `0` represents water.

An **island** is a 4-directionally connected group of `1`'s not connected to any other `1`'s. There are **exactly two islands** in `grid`.

You may change `0`'s to `1`'s to connect the two islands to form **one island**.

Return _the smallest number of_ `0`_'s you must flip to connect the two islands_.

## solution

Add every cell of the first island to a queue and `seen` set, and then BFS towards the other island. Return the depth the first time that we reach the next island.

```python
class Solution:
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	  
	def initializeFirstIsland(self, grid):
		n = len(grid)
		seen = set()
		q = deque()
		  
		def dfs(x, y):
			seen.add((x, y))
			q.append((x, y))
			  
			for dx, dy in self.dirs:
				nx, ny = x+dx, y+dy
			  
				if 0 <= nx < n and 0 <= ny < n:
					if grid[nx][ny] == 1 and (nx, ny) not in seen:
						seen.add((nx, ny))
						dfs(nx, ny)
		  
		for i in range(n):
			for j in range(n):
				if grid[i][j] == 1:
					dfs(i, j)
					return seen, q
  
def shortestBridge(self, grid: List[List[int]]) -> int:
	n = len(grid)
	  
	seen, q = self.initializeFirstIsland(grid)
	  
	depth = 0
	while q:
		level_len = len(q)
		  
		for _ in range(level_len):
			x, y = q.popleft()
		  
			for dx, dy in self.dirs:
				nx, ny = x+dx, y+dy
		  
				if 0 <= nx < n and 0 <= ny < n:
					if (nx, ny) not in seen:
						if grid[nx][ny] == 1:
							return depth
						seen.add((nx, ny))
						q.append((nx, ny))
		depth += 1
```
