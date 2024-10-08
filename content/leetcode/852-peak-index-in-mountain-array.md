---
type: leetcode
title: 852. peak index in mountain array
tags:
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-06
updated: 2024-10-06
---

You are given an integer **mountain** array `arr` of length `n` where the values increase to a **peak element** and then decrease.

Return the index of the peak element.

Your task is to solve it in `O(log(n))` time complexity.

## solution

Basic modified binary search.

```python
def peakIndexInMountainArray(self, arr: List[int]) -> int:
	n = len(arr)
	l, r = 1, n-2
	  
	while l <= r:
		m = (l+r)//2
	  
		if arr[m-1] < arr[m] > arr[m+1]:
			return m
		elif arr[m-1] < arr[m] < arr[m+1]:
			l = m+1
		else:
			r = m-1
	return -1
```
