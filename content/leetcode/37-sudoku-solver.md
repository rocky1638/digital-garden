---
type: leetcode
title: 37. sudoku solver
tags:
  - backtracking
  - hashmap
aliases: 
parents:
  - "[[36-valid-sudoku]]"
children: 
supports: 
enemies: 
date: 2024-08-06
updated: 2024-08-06
---

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

1. Each of the digits `1-9` must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

The `'.'` character indicates empty cells.

## solution

Trying to convert the solution from [[36-valid-sudoku]] into this solution is a little bit of a trap. We want to find something more efficient than checking the entire puzzle at each iteration when we’re backtracking.

Instead, we want to keep sets to store what unique values are in each row, column, and square. Then, keeping track of all the slots that we still need to fill, we try to fill the next one with a valid value at each backtracking step.

```python
from collections import defaultdict, deque

def solveSudoku(self, board: List[List[str]]) -> None:
	sets = defaultdict(set)
	empty = deque()

	# Initialize sets for rows, columns, and 3x3 blocks
	for i in range(9):
		for j in range(9):
			if board[i][j] != ".":
				num = board[i][j]

				sets[f"r{i}"].add(num) # Row set
				sets[f"c{j}"].add(num) # Column set
				sets[f"sq{i//3}{j//3}"].add(num) # 3x3 block set
			else:
				empty.append((i, j))

	# Define backtrack function to recursively solve Sudoku
	def backtrack():
		if not empty: # Check if there are no more empty cells to fill
			return True

		x, y = empty[0]
		# Try placing each number from '1' to '9' in the empty cell
		for num in {'1', '2', '3', '4', '5', '6', '7', '8', '9'}:
			if (
				num not in sets[f"r{x}"]
				and num not in sets[f"c{y}"]
				and num not in sets[f"sq{x//3}{y//3}"]
			):
				# Place the number and update sets
				board[x][y] = num
				sets[f"r{x}"].add(num)
				sets[f"c{y}"].add(num)
				sets[f"sq{x//3}{y//3}"].add(num)
				empty.popleft()
				# Recursively attempt to solve Sudoku
				if backtrack():
					return True
				else:
				# Backtrack if placing num does not lead to a solution
				board[x][y] = "."
				sets[f"r{x}"].remove(num)
				sets[f"c{y}"].remove(num)
				sets[f"sq{x//3}{y//3}"].remove(num)
				empty.appendleft((x, y))
		return False

	# Start solving Sudoku from the first empty cell
	backtrack()
```
