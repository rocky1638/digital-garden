---
type: leetcode
title: 529. minesweeper
tags:
  - recursion
  - simulation
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-17
updated: 2024-10-17
---

Let's play the minesweeper game ([Wikipedia](https://en.wikipedia.org/wiki/Minesweeper_(video_game)), [online game](http://minesweeperonline.com/))!

You are given an `m x n` char matrix `board` representing the game board where:

- `'M'` represents an unrevealed mine,
- `'E'` represents an unrevealed empty square,
- `'B'` represents a revealed blank square that has no adjacent mines (i.e., above, below, left, right, and all 4 diagonals),
- digit (`'1'` to `'8'`) represents how many mines are adjacent to this revealed square, and
- `'X'` represents a revealed mine.

You are also given an integer array `click` where `click = [clickr, clickc]` represents the next click position among all the unrevealed squares (`'M'` or `'E'`).

Return _the board after revealing this position according to the following rules_:

1. If a mine `'M'` is revealed, then the game is over. You should change it to `'X'`.
2. If an empty square `'E'` with no adjacent mines is revealed, then change it to a revealed blank `'B'` and all of its adjacent unrevealed squares should be revealed recursively.
3. If an empty square `'E'` with at least one adjacent mine is revealed, then change it to a digit (`'1'` to `'8'`) representing the number of adjacent mines.
4. Return the board when no more squares will be revealed.

## solution

Just use recursion and follow the instructions.

```python
def updateBoard(self, board: List[List[str]], click: List[int]) -> List[List[str]]:
	m, n = len(board), len(board[0])
	dirs = [[0,1],[1,0],[0,-1],[-1,0],[1,1],[1,-1],[-1,1],[-1,-1]]
	  
	revealed = [[False]*n for _ in range(m)]
	  
	def num_adjacent_mines(x, y):
		res = 0
		for dx, dy in dirs:
			nx, ny = x+dx, y+dy
			if 0 <= nx < m and 0 <= ny < n:
				if board[nx][ny] == "M":
					res += 1
		return res
	  
	def reveal(x, y):
		if x < 0 or x >= m or y < 0 or y >= n:
			return
		if revealed[x][y]:
			return

		if board[x][y] == "M":
			board[x][y] = "X"
			return
		if board[x][y] == "E":
			num_mines = num_adjacent_mines(x, y)
			# no adjacent mines
			if num_mines == 0:
				board[x][y] = "B"
				revealed[x][y] = True
				# reveal adjacent
				for dx, dy in dirs:
					reveal(x+dx, y+dy)
			else:
				board[x][y] = str(num_mines)
				revealed[x][y] = True
	  
	reveal(click[0], click[1])
```
