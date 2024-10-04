---
type: leetcode
title: 1539. kth missing positive number
tags:
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-09-16
---

Given an array `arr` of positive integers sorted in a **strictly increasing order**, and an integer `k`.

Return _the_ `kth` _**positive** integer that is **missing** from this array._

## solutions

### linear scan

Once we figure out the intuition that the number of missing numbers at an index $i$ is equal to `arr[i]-i-1`, we can just scan and search for the first value that has $\ge k$ missing numbers.

```python
def findKthPositive(self, arr: List[int], k: int) -> int:
	for i in range(len(arr)):
		num_missing = arr[i] - i - 1
	  
		if num_missing >= k:
			return k + i
	return k + len(arr)
```

### binary search

Instead of scanning linearly, we can find this correct index with binary search (more specifically, `bisect_left`.)

```python
def findKthPositive(self, arr: List[int], k: int) -> int:
	l, r = 0, len(arr)
	  
	# bisect_left
	while l < r:
		m = (l+r)//2
	  
		num_missing = arr[m] - m - 1
		if num_missing >= k:
			r = m
		else:
			l = m+1
	  
	return k + l
```
