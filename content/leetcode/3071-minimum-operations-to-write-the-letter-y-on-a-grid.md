---
type: leetcode
title: 3071. minimum operations to write the letter y on a grid
tags:
  - matrix
  - math
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-08
updated: 2024-08-08
---

You are given a **0-indexed** `n x n` grid where `n` is odd, and `grid[r][c]` is `0`, `1`, or `2`.

We say that a cell belongs to the Letter **Y** if it belongs to one of the following:

- The diagonal starting at the top-left cell and ending at the center cell of the grid.
- The diagonal starting at the top-right cell and ending at the center cell of the grid.
- The vertical line starting at the center cell and ending at the bottom border of the grid.

The Letter **Y** is written on the grid if and only if:

- All values at cells belonging to the Y are equal.
- All values at cells not belonging to the Y are equal.
- The values at cells belonging to the Y are different from the values at cells not belonging to the Y.

Return _the **minimum** number of operations needed to write the letter Y on the grid given that in one operation you can change the value at any cell to_ `0`_,_ `1`_,_ _or_ `2`_._

## solutions

Figure out general expressions for the coordinates of a Y, and then store frequencies in two counters.

Instead of figuring out some complex logic for which number swaps are optimal, just try every single one as there’s only six possibilities _(3 possibilities for the Y, and 2 for the non-Y out of the remaining numbers)_.

```python
def minimumOperationsToWriteY(self, grid: List[List[int]]) -> int:
	"""
	left slant: x,x for x in range(0, n//2-1)
	right slant: x,(n-1-x) for x in range(0, n//2-1)
	center: (x//2, x//2)
	vertical: x, n//2 for x in range(n//2+1, n-1)
	"""
	n = len(grid)
	  
	yFreq = Counter()
	nonYFreq = Counter()
	  
	for i in range(n):
		for j in range(n):
			# left slant
			if i == j and i < n//2:
				yFreq[grid[i][j]] += 1
			# right slant
			elif i == (n-1-j) and i < n // 2:
				yFreq[grid[i][j]] += 1
			# center
			elif i == j and i == n//2:
				yFreq[grid[i][j]] += 1
			# vertical
			elif j == n//2 and n//2+1 <= i <= n-1:
				yFreq[grid[i][j]] += 1
			else:
				nonYFreq[grid[i][j]] += 1

	ans = inf
	for x in range(3): # choice for Y
		for y in range(3): # choice for non-Y
			if x == y:
				continue
			y_changes = yFreq.total() - yFreq[x]
			non_y_changes = nonYFreq.total() - nonYFreq[y]
	  
	ans = min(ans, y_changes+non_y_changes)
	
	return ans
```
