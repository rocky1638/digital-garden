---
type: leetcode
title: 1162. as far from land as possible
tags:
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-04-12
---

Given an `n x n` `grid` containing only values `0` and `1`, where `0` represents water and `1` represents land, find a water cell such that its distance to the nearest land cell is maximized, and return the distance. If no land or water exists in the grid, return `-1`.

The distance used in this problem is the Manhattan distance: the distance between two cells `(x0, y0)` and `(x1, y1)` is `|x0 - x1| + |y0 - y1|`.

## solution

```python
def maxDistance(self, grid: List[List[int]]) -> int:
	"""
	- add all land coords to BFS queue
	- in parallel, bfs from all land into water
	"""
	  
	n = len(grid)
	q = deque()
	  
	# initialize BFS queue with land cells
	for i in range(n):
		for j in range(n):
			if grid[i][j] == 1:
				q.append((i, j))

	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	seen = set()
	depth = 0
	  
	while q:
		level_len = len(q)
		for i in range(level_len):
			x, y = q.popleft()
	  
			for d in dirs:
				nx, ny = x+d[0], y+d[1]
				if nx >= 0 and nx < n and ny >= 0 and ny < n:
					if (nx, ny) not in seen and grid[nx][ny] != 1:
						q.append((nx, ny))
						seen.add((nx, ny))
		depth += 1
	  
	return depth - 1 if depth > 1 else -1
```
