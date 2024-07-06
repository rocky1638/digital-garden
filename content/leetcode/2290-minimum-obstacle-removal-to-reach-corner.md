---
type: leetcode
title: 2290. minimum obstacle removal to reach corner
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-05-28
---

You are given a **0-indexed** 2D integer array `grid` of size `m x n`. Each cell has one of two values:

- `0` represents an **empty** cell,
- `1` represents an **obstacle** that may be removed.

You can move up, down, left, or right from and to an empty cell.

Return _the **minimum** number of **obstacles** to **remove** so you can move from the upper left corner_ `(0, 0)` _to the lower right corner_ `(m - 1, n - 1)`.

## solutions

The intuition to simplify this problem is to think of the maze as a weighted graph, where travelling to an obstacle has a cost of 1, whereas going to an empty square has a cost of 0.

### dfs with accumulator

We can simply brute-force all of the possible paths, keeping track of the cost of of traversal and which nodes we’ve visited so far.

This has an exponential runtime as for each cell, we can travel to four other cells, which would be $O(4^{mn})$.

### djikstra’s algorithm

```python
def minimumObstacles(self, grid: List[List[int]]) -> int:
	m, n = len(grid), len(grid[0])
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	dist = [[inf]*n for _ in range(m)]
	dist[0][0] = 0
	pq = [(0,0,0)]
	  
	while pq:
		cost, x, y = heappop(pq)
		if x == m-1 and y == n-1:
			return cost
		for d in dirs:
			nx, ny = x+d[0], y+d[1]
			if nx >= 0 and nx < m and ny >= 0 and ny < n:
				if cost + grid[nx][ny] < dist[nx][ny]:
					dist[nx][ny] = cost + grid[nx][ny]
					heappush(pq, (dist[nx][ny], nx, ny))
```

### 0-1 BFS
