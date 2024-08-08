---
type: leetcode
title: 1428. leftmost column with one
tags:
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-01
---

A **row-sorted binary matrix** means that all elements are `0` or `1` and each row of the matrix is sorted in non-decreasing order.

Given a **row-sorted binary matrix** `binaryMatrix`, return _the index (0-indexed) of the **leftmost column** with a 1 in it_. If such an index does not exist, return `-1`.

**You can't access the Binary Matrix directly.** You may only access the matrix using a `BinaryMatrix` interface:

- `BinaryMatrix.get(row, col)` returns the element of the matrix at index `(row, col)` (0-indexed).
- `BinaryMatrix.dimensions()` returns the dimensions of the matrix as a list of 2 elements `[rows, cols]`, which means the matrix is `rows x cols`.

Submissions making more than `1000` calls to `BinaryMatrix.get` will be judged _Wrong Answer_. Also, any solutions that attempt to circumvent the judge will result in disqualification.

For custom testing purposes, the input will be the entire binary matrix `mat`. You will not have access to the binary matrix directly.

## solution

We just binary search each row of the matrix for the leftmost one. The “find left-bound” template being used here is the same one described in [[binary-search#template for “find leftmost that satisfies condition”]].

```python
def leftMostColumnWithOne(self, binaryMatrix: 'BinaryMatrix') -> int:
m, n = binaryMatrix.dimensions()
  
def binsearch(row_idx):
	l, r = 0, n
	while l < r:
		m = l+(r-l)//2
  
		if binaryMatrix.get(row_idx, m) == 1:
			r = m
		else:
			l = m+1
	return l

ans = n
for i in range(m):
	ans = min(ans, binsearch(i))
return ans if ans < n else -1
```
