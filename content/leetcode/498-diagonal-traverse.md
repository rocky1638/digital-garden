---
type: leetcode
title: 498. diagonal traverse
tags:
  - matrix
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-01
updated: 2024-09-01
---

Given an `m x n` matrix `mat`, return _an array of all the elements of the array in a diagonal order_.

![[498-diagonal-traverse.png]]

## solution

Nothing fancy, just draw out and figure out how to move the cursor.

Perhaps another way to do this is to do every diagonal in one direction, then reverse every other one.

```python
def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
	res = []
	m, n = len(mat), len(mat[0])
	  
	def down_diagonal(x, y):
		while x+1 < m and y-1 >= 0:
			res.append(mat[x][y])
			x += 1
			y -= 1
	  
		res.append(mat[x][y])

		# try move down, else right
		if x+1 < m:
			return x+1, y
		return x, y+1
	  
	def up_diagonal(x, y):
		while x-1 >= 0 and y+1 < n:
			res.append(mat[x][y])
			x -= 1
			y += 1
	  
		# now standing on last value in diagonal
		res.append(mat[x][y])

		# try move right, else down
		if y+1 < n:
			return x, y+1
		return x+1, y
	  
	i = j = 0
	num_diags = m+n-1
	for _ in range((num_diags)//2):
		i, j = up_diagonal(i, j)
		i, j = down_diagonal(i, j)
		  
	if num_diags & 1:
		down_diagonal(i, j)

	return res
```
