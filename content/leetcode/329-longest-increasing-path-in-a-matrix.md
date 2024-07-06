---
title: 329. longest increasing path in a matrix
date: 2022-12-25
updated: 2024-05-29
---

Given an `m x n` integers `matrix`, return _the length of the longest increasing path in_ `matrix`.

From each cell, you can either move in four directions: left, right, up, or down. You **may not** move **diagonally** or move **outside the boundary** (i.e., wrap-around is not allowed).

## solutions

### dfs w/ memoization

Initially, I thought that we needed to do something fancy because a simple DFS + memoization wouldn’t work, as we would need to memoize a `visited` array as well.

However, a big realization here is that the `visited` array is unnecessary as our valid paths are necessary monotonically increasing, meaning that it’s impossible to visit a node that’s already been visited.

As such, a simple DFS solution with memoization works here.

```python
def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
	m, n = len(matrix), len(matrix[0])
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	memo = {}
	  
	def dfs(x, y):
		if (x, y) in memo:
			return memo[(x, y)]

		best_subpath = 0
		for d in dirs:
			nx, ny = x+d[0], y+d[1]
			if 0 <= nx < m and 0 <= ny < n:
				if matrix[nx][ny] > matrix[x][y]:
					best_subpath = max(best_subpath, dfs(nx, ny))
	  
		memo[(x, y)] = best_subpath + 1
		return memo[(x, y)]

	ans = 0
	for i in range(m):
		for j in range(n):
			ans = max(ans, dfs(i, j))
	  
	return ans
```

### bfs w/ topological sort

Another way this question can be solved is by imagining the matrix as a directed acyclic graph, where directed edges exist from adjacent cells $x$ to $y$ when $x \lt y$.

```python
def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
	m, n = len(matrix), len(matrix[0])
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	indegrees = Counter()
	memo = {}
	  
	# construct indegrees
	for x in range(m):
		for y in range(n):
			for dx, dy in dirs:
				nx, ny = x+dx, y+dy
				if 0 <= nx < m and 0 <= ny < n:
					if matrix[nx][ny] > matrix[x][y]:
						indegrees[(nx, ny)] += 1

	# initialize queue with 0 indegree nodes
	q = deque()
	for x in range(m):
		for y in range(n):
			if indegrees[(x, y)] == 0:
				q.append((x, y))
	  
	ans = 0
	while q:
		level_len = len(q)
	  
		for _ in range(level_len):
			x, y = q.popleft()
			for dx, dy in dirs:
				nx, ny = x+dx, y+dy
				if 0 <= nx < m and 0 <= ny < n:
					if matrix[nx][ny] > matrix[x][y]:
						indegrees[(nx, ny)] -= 1
						if indegrees[(nx, ny)] == 0:
							q.append((nx, ny))

		ans += 1
	  
	return ans
```
