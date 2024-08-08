---
type: leetcode
title: 36. valid sudoku
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-05
updated: 2024-08-05
---

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

## solution

For each row, column, and square, check for valid state.

```python
def isValidSudoku(self, board: List[List[str]]) -> bool:
	def is_valid_row(i):
		filtered = list(filter(lambda x: x != ".", board[i]))
		return len(filtered) == len(set(filtered))
	  
	def is_valid_col(j):
		col = [row[j] for row in board]
		filtered = list(filter(lambda x: x != ".", col))
		return len(filtered) == len(set(filtered))
	  
	def is_valid_square(r, c):
		seen = set()
		for i in range(r*3, r*3+3):
			for j in range(c*3, c*3+3):
				if board[i][j] != ".":
					if board[i][j] in seen:
						return False
					seen.add(board[i][j])
		return True

	m, n = len(board), len(board[0])
	valid = True
	for i in range(m):
		valid = valid and is_valid_row(i)
	for j in range(n):
		valid = valid and is_valid_col(j)
	for r in range(3):
		for c in range(3):
			valid = valid and is_valid_square(r, c)
	return valid
```
