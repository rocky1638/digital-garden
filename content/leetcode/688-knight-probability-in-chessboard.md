---
type: leetcode
title: 688. knight probability in chessboard
tags:
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-04-28
---

On an `n x n` chessboard, a knight starts at the cell `(row, column)` and attempts to make exactly `k` moves. The rows and columns are **0-indexed**, so the top-left cell is `(0, 0)`, and the bottom-right cell is `(n - 1, n - 1)`.

A chess knight has eight possible moves it can make, as illustrated below. Each move is two cells in a cardinal direction, then one cell in an orthogonal direction.

![](https://assets.leetcode.com/uploads/2018/10/12/knight.png)

Each time the knight is to move, it chooses one of eight possible moves uniformly at random (even if the piece would go off the chessboard) and moves there.

The knight continues moving until it has made exactly `k` moves or has moved off the chessboard.

Return _the probability that the knight remains on the board after it has stopped moving_.

## solution

We can simulate the knight moves using a breadth-first search. By the time we do `k` iterations, we want to see how many valid paths are still in our queue. This value, divided by the total number of possible paths, $8^k$, is our probability.

The interesting optimization here is to use a frequency dictionary instead of a list to store our BFS state, in order to more efficiently deal with duplicate positions amongst our paths.

```python
def knightProbability(self, n: int, k: int, row: int, column: int):
	dirs = [[-1,-2],[-2,-1],[-2,1],[-1,2],[1,2],[2,1],[2,-1],[1,-2]]
	q = {(row,column): 1}
	level = 0
	
	while q and level < k:
		next_level = {}
	
		for key in q:
			x, y = key
			freq = q[key]
		
			for d in dirs:
				nx, ny = x+d[0], y+d[1]
				if not (nx < 0 or nx >= n or ny < 0 or ny >= n):
					if (nx,ny) in next_level:
						next_level[(nx,ny)] += freq
					else:
						next_level[(nx,ny)] = freq
	
		level += 1
		q = next_level
	
	return sum(q.values()) / (8**k)
```
