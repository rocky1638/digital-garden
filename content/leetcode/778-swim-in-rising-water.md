---
type: leetcode
title: 778. swim in rising water
tags:
  - djikstra
  - graph
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-04
---


You are given an `n x n` integer matrix `grid` where each value `grid[i][j]` represents the elevation at that point `(i, j)`.

The rain starts to fall. At time `t`, the depth of the water everywhere is `t`. You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares individually are at most `t`. You can swim infinite distances in zero time. Of course, you must stay within the boundaries of the grid during your swim.

Return _the least time until you can reach the bottom right square_ `(n - 1, n - 1)` _if you start at the top left square_ `(0, 0)`.

## solution

We realize that this is a variation of [[djikstras-algorithm]], where we want to find the “shortest” path to the bottom-right corner. However, the shortest path in this case is not the sum of weights of all edges used, but instead just the highest valued node that we pass through in the path.

So, everytime we add a value to our frontier, we want to add the maximum of it and the biggest value that it has seen in its path so far.

> [!attention]
> Normally with Djikstra, we can only mark a node as visited once we have dequeued it from the queue, as the first time we add it to the queue might not be the shortest path to that node.
>
> However, the nature of what we’re optimizing in this problem (the maximum value in a given path), along with using a priority queue, means that the first time we enqueue a node is guaranteed to be the best path that node belongs to.
>
> This is because if we were to reach this square $i$ in the future in some other path, this path will have already contained some heights equal to or greater than the height of $i$ (because our BFS visits nodes that are monotonically increasing in height). In other words, it’s impossible for future paths that visit this node to improve on the value for square $i$.

```python
def swimInWater(self, grid: List[List[int]]) -> int:
	n = len(grid)
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	  
	q = [(grid[0][0], 0, 0)]
	seen = set([(0,0)])
	  
	while q:
		cost, x, y = heappop(q)
		if x == n-1 and y == n-1:
			return cost
	  
		for dx, dy in dirs:
			nx, ny = x+dx, y+dy
			if 0 <= nx < n and 0 <= ny < n:
				if (nx, ny) not in seen:
					seen.add((nx, ny))
					heappush(q, (max(cost, grid[nx][ny]), nx, ny))
```

### bonus: print optimal path

If we maintain a `prev` matrix, we can walk through the matrix to print our optimal path.

```python
def swimInWater(self, grid: List[List[int]]) -> int:
	n = len(grid)
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	prev = [[None for _ in range(n)] for _ in range(n)]
	  
	q = [(grid[0][0], 0, 0)]
	seen = set([(0,0)])

	ans = 0
	while q:
		cost, x, y = heappop(q)
		if x == n-1 and y == n-1:
			ans = cost
			break
	  
		for dx, dy in dirs:
			nx, ny = x+dx, y+dy
			if 0 <= nx < n and 0 <= ny < n:
				if (nx, ny) not in seen:
					seen.add((nx, ny))
					prev[nx][ny] = (x, y)
					heappush(q, (max(cost, grid[nx][ny]), nx, ny))

	path = []
	i, j = n-1, n-1
	while True:
		if i == j == 0:
			break
		path.append(grid[i][j])
		i, j = prev[i][j]
	print(path + [grid[0][0]])

	return ans
```
