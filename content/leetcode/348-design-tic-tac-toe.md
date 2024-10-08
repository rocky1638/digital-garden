---
type: leetcode
title: 348. design tic tac toe
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-11
updated: 2024-09-11
---

Assume the following rules are for the tic-tac-toe game on an `n x n` board between two players:

1. A move is guaranteed to be valid and is placed on an empty block.
2. Once a winning condition is reached, no more moves are allowed.
3. A player who succeeds in placing `n` of their marks in a horizontal, vertical, or diagonal row wins the game.

Implement the `TicTacToe` class:

- `TicTacToe(int n)` Initializes the object the size of the board `n`.
- `int move(int row, int col, int player)` Indicates that the player with id `player` plays at the cell `(row, col)` of the board. The move is guaranteed to be a valid move, and the two players alternate in making moves. Return
    - `0` if there is **no winner** after the move,
    - `1` if **player 1** is the winner after the move, or
    - `2` if **player 2** is the winner after the move.

## solution

The logic for the optimization here is basically identical to the one used in [[37-sudoku-solver]].

```python
class TicTacToe:
	def __init__(self, n: int):
		self.n = n
		self.rows = [[0,0] for _ in range(n)]
		self.cols = [[0,0] for _ in range(n)]
		# [ascending, descending]
		self.diags = [[0,0] for _ in range(2)]
	  
	def move(self, row: int, col: int, player: int) -> int:
		self.rows[row][player-1] += 1
		self.cols[col][player-1] += 1
	  
		if row == col:
			self.diags[1][player-1] += 1
		if row+col == self.n-1:
			self.diags[0][player-1] += 1

		if (
			self.rows[row][player-1] == self.n
			or self.cols[col][player-1] == self.n
			or self.diags[0][player-1] == self.n
			or self.diags[1][player-1] == self.n
		):
			return player
		return 0
```
