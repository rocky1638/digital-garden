---
title: 54. spiral matrix
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/spiral-matrix/
date: 2022-11-22
updated: 2024-08-23
tags:
  - geometry
---

Given an `m x n` `matrix`, return _all elements of the_ `matrix` _in spiral order_.

## solution

We keep track of which direction we’re moving in, and turn the next direction when we hit the edge of the matrix or some cell that we’ve already added to `output`.

To know what we’ve already seen, we can either use a `seen` set which uses $O(mn)$ space, or just modify the matrix in-place after we add a value to the `output` array.

```python
class Solution:
	def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
		m, n = len(matrix), len(matrix[0])
		dirs = [[0,1],[1,0],[0,-1],[-1,0]]
		# go in order of dirs, move to next direction once we see border or seen
		seen = set()
		ans = []
		cd = 0
		
		i, j = 0, 0
		
		for _ in range(m*n):
			ans.append(matrix[i][j])
			seen.add((i,j))
		
			ni, nj = i + dirs[cd][0], j + dirs[cd][1]
			if ni >= 0 and ni < m and nj >= 0 and nj < n and (ni,nj) not in seen:
				# if valid and unseen, move to it
				i, j = ni, nj
			else:
				cd = (cd + 1) % 4
				ni, nj = i + dirs[cd][0], j + dirs[cd][1]
				i, j = ni, nj
		
		return ans
```
