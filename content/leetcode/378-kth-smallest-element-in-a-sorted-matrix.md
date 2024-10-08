---
type: leetcode
title: 378. kth smallest element in a sorted matrix
tags:
  - heap
  - binary-search
aliases: 
parents:
  - "[[23-merge-k-sorted-lists]]"
children: 
supports: 
enemies: 
date: 2024-09-21
updated: 2024-09-21
---

Given an `n x n` `matrix` where each of the rows and columns is sorted in ascending order, return _the_ `kth` _smallest element in the matrix_.

Note that it is the `kth` smallest element **in the sorted order**, not the `kth` **distinct** element.

You must find a solution with a memory complexity better than `O(n2)`.

## solution

We can solve this the same way as [[23-merge-k-sorted-lists]].

```python
# O(klogn + n) -> as k approaches n, O(nlogn)
def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
	n = len(matrix)
	min_heap = []

	# add head of each list
	for i in range(n):
		heappush(min_heap, (matrix[i][0], i, 0))

	for _ in range(k-1):
		_, row, col = heappop(min_heap)
		if col+1 < n:
			heappush(min_heap, (matrix[row][col+1], row, col+1))
	return heappop(min_heap)[0]
```
