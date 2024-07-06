---
title: 286. walls and gates
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/walls-and-gates/
date: 2023-01-13
updated: 2024-06-04
tags:
  - bfs
---

You are given an `m x n` grid `rooms` initialized with these three possible values.

- `-1` A wall or an obstacle.
- `0` A gate.
- `INF` Infinity means an empty room. We use the value `231 - 1 = 2147483647` to represent `INF` as you may assume that the distance to a gate is less than `2147483647`.

Fill each empty room with the distance to _its nearest gate_. If it is impossible to reach a gate, it should be filled with `INF`.

![](https://assets.leetcode.com/uploads/2021/01/03/grid.jpg)

## solution

We BFS in parallel from all of the gates.

The first time we reach a cell, we must have reached it from the closest gate to it because all the traversals are moving outwards at the same rate.

```python
def wallsAndGates(self, rooms: List[List[int]]) -> None:
	m, n = len(rooms), len(rooms[0])
	INF = 2147483647
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]

	# start bfs from empty rooms
	q = collections.deque()
	for i in range(m):
		for j in range(n):
			if rooms[i][j] == 0:
				q.append((i, j, 0))
	
	while q:
		i, j, dist = q.popleft()
		for d in dirs:
			ni, nj = i + d[0], j + d[1]
	
			if m > ni >= 0 and n > nj >= 0:
				if rooms[ni][nj] == INF:
					rooms[ni][nj] = dist + 1
					q.append((ni, nj, dist + 1))
```
