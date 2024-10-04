---
type: leetcode
title: 419. battleships in a board
tags:
  - bfs
  - dfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-15
updated: 2024-09-15
---

Given an `m x n` matrix `board` where each cell is a battleship `'X'` or empty `'.'`, return _the number of the **battleships** on_ `board`.

**Battleships** can only be placed horizontally or vertically on `board`. In other words, they can only be made of the shape `1 x k` (`1` row, `k` columns) or `k x 1` (`k` rows, `1` column), where `k` can be of any size. At least one horizontal or vertical cell separates between two battleships (i.e., there are no adjacent battleships).

## solutions

### sink islands

Solve it exactly the same way as [[200-number-of-islands]].

```python
def countBattleships(self, board: List[List[str]]) -> int:
	m, n = len(board), len(board[0])
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	  
	def sink(i, j):
		board[i][j] = ""
		q = deque([(i, j)])
	  
		while q:
			x, y = q.popleft()
		  
			for dx, dy in dirs:
				nx, ny = x+dx, y+dy
	  
				if 0 <= nx < m and 0 <= ny < n:
					if board[nx][ny] == "X":
						board[nx][ny] = ""
						q.append((nx, ny))
	  
	res = 0
	for i in range(m):
		for j in range(n):
			if board[i][j] == "X":
				sink(i, j)
				res += 1
	return res
```

### constant space

Instead of sinking the battleships, we need to figure out how to know if we’ve already counted an “X” as part of another battleship when we’re iterating through the matrix.

The intution here is that if we traverse left-to-right, top-to-bottom, only the first square of a battleship should be counted. Because no battleships touch or overlap, we know that only the first square will both have the upper and leftward squares be empty (draw this out to visualize it).

```python
def countBattleships(self, board: List[List[str]]) -> int:
	m, n = len(board), len(board[0])
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	res = 0
	  
	def is_first(x, y):
		up = (x-1, y)
		left = (x, y-1)
	  
		if x-1 < 0 or board[x-1][y] == ".":
			if y-1 < 0 or board[x][y-1] == ".":
				return True
		return False
	  
	for i in range(m):
		for j in range(n):
			if board[i][j] == "X":
				if is_first(i, j):
					res += 1
	return res
```
