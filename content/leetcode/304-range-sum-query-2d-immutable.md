---
type: leetcode
title: 304. range sum query 2d - immutable
tags:
  - prefix-sums
  - geometry
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-19
---

Given a 2D matrix `matrix`, handle multiple queries of the following type:

- Calculate the **sum** of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.

Implement the `NumMatrix` class:

- `NumMatrix(int[][] matrix)` Initializes the object with the integer matrix `matrix`.
- `int sumRegion(int row1, int col1, int row2, int col2)` Returns the **sum** of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.

You must design an algorithm where `sumRegion` works on `O(1)` time complexity.

## solution

We pre-compute the “suffix sum” of all squares rooted at a top-left corner $(x, y)$ and extending to the bottom-right corner.

With these numbers, we can calculate the sum of any rectangle buy doing some intersecting and subtracting with smaller rectangles, as described in the `sumRegion` method.

```python
class NumMatrix:
	def __init__(self, matrix: List[List[int]]):
		self.m, self.n = len(matrix), len(matrix[0])
		# { (x, y): sum from cell to bottom right }
		self.sums = [[0 for _ in range(self.n+1)] for _ in range(self.m+1)]

		# sum every sum from every cell -> bottom right
		for i in reversed(range(self.m)):
			row_acc = 0
			for j in reversed(range(self.n)):
				row_acc += matrix[i][j]
				self.sums[i][j] = row_acc
				if i < (self.m-1):
					self.sums[i][j] += self.sums[i+1][j]
	
	
	def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
		# sum from top left - bottom left - top right + bottom right
		# (because we subtract it twice)
		top_left = self.sums[row1][col1]
		bottom_left = self.sums[row2+1][col1]
		top_right = self.sums[row1][col2+1]
		bottom_right = self.sums[row2+1][col2+1]
		return top_left - bottom_left - top_right + bottom_right

```
