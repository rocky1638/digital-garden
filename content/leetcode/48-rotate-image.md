---
type: leetcode
title: 48. rotate image
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/rotate-image/
date: 2022-12-27
updated: 2024-09-01
tags:
  - array
  - matrix
---

You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

## solutions

### logical

Literally just matrix logic. We keep four pointers starting on each corner of each layer, and move our pointers along the sides.

```python
def rotate(self, matrix: List[List[int]]) -> None:
	"""
	Do not return anything, modify matrix in-place instead.
	"""
	n = len(matrix)
	its = n // 2
	
	for it in range(its):
		tl = [0 + it, 0 + it]
		tr = [0 + it, n - 1 - it]
		bl = [n - 1 - it, 0 + it]
		br = [n - 1 - it, n - 1 - it]
		
		for _ in range(n-1-(2*it)):
			tr_temp = matrix[tr[0]][tr[1]]
			matrix[tr[0]][tr[1]] = matrix[tl[0]][tl[1]]
			matrix[tl[0]][tl[1]] = matrix[bl[0]][bl[1]]
			matrix[bl[0]][bl[1]] = matrix[br[0]][br[1]]
			matrix[br[0]][br[1]] = tr_temp
			
			tl[1] += 1
			tr[0] += 1
			br[1] -= 1 
			bl[0] -= 1
```

### reverse + reflect

Kinda just have to draw this one out…

```python
def rotate(self, matrix: List[List[int]]) -> None:
	"""
	1. reverse
	2. reflect
	for an index (i, j), reflection index is (n-1-j, n-1-i)
	"""
	  
	n = len(matrix)

	def reverse(row):
		l, r = 0, n-1
		while l < r:
			row[l], row[r] = row[r], row[l]
			l += 1
			r -= 1
	  
	# reverse
	for row in matrix:
		reverse(row)

	# reflect over /
	for i in range(n-1):
		for j in range(n-i-1):
			matrix[i][j], matrix[n-j-1][n-i-1] = matrix[n-j-1][n-i-1], matrix[i][j]
```
