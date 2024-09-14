---
type: leetcode
title: 317. shortest distance from all buildings
tags:
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-11
updated: 2024-09-11
---

You are given an `m x n` grid `grid` of values `0`, `1`, or `2`, where:

- each `0` marks **an empty land** that you can pass by freely,
- each `1` marks **a building** that you cannot pass through, and
- each `2` marks **an obstacle** that you cannot pass through.

You want to build a house on an empty land that reaches all buildings in the **shortest total travel** distance. You can only move up, down, left, and right.

Return _the **shortest travel distance** for such a house_. If it is not possible to build such a house according to the above rules, return `-1`.

The **total travel distance** is the sum of the distances between the houses of the friends and the meeting point.

The distance is calculated using [Manhattan Distance](http://en.wikipedia.org/wiki/Taxicab_geometry), where `distance(p1, p2) = |p2.x - p1.x| + |p2.y - p1.y|`.

## solutions

Several insights:

1. BFS (shortest path) from all buildings (`1`) to every empty cell.
2. Keep track of the total depth in another matrix `distances`.
3. Also, keep track of the number of BFS runs that successfully reach each empty square. We can only return the distances from squares that are reachable by all houses.

```python
def shortestDistance(self, grid: List[List[int]]) -> int:
	m, n = len(grid), len(grid[0])
	num_houses = 0
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	  
	# create array to sum up BFS depths
	# starting from each house
	# (total_distance, num_houses)
	distances = [[[0, 0] for _ in range(n)] for _ in range(m)]
	for i in range(m):
		for j in range(n):
			if grid[i][j] != 0:
				distances[i][j] = [inf, inf]
				if grid[i][j] == 1:
					num_houses += 1

	def bfs(i, j):
		seen = set()
		seen.add((i, j))
		q = deque([(i, j)])
		depth = 0
	  
		while q:
		level_len = len(q)
	  
		for _ in range(level_len):
			x, y = q.popleft()
			distances[x][y][0] += depth
			distances[x][y][1] += 1
	  
			for dx, dy in dirs:
				nx, ny = x+dx, y+dy
	  
				if 0 <= nx < m and 0 <= ny < n and (nx, ny) not in seen:
					if grid[nx][ny] == 0:
						seen.add((nx, ny))
						q.append((nx, ny))
		depth += 1
	  
	# BFS, incrementing total min distance from each house
	for x in range(m):
		for y in range(n):
			if grid[x][y] == 1:
				bfs(x, y)

	# find smallest value that's > num_houses
	res = inf
	for x in range(m):
		for y in range(n):
			if distances[x][y][1] == num_houses:
				res = min(res, distances[x][y][0])
	return -1 if res == inf else res
```
