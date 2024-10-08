---
type: leetcode
title: 162. find peak element
tags:
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-10
updated: 2024-08-10
---

A peak element is an element that is strictly greater than its neighbors.

Given a **0-indexed** integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

## solution

Just a custom binary search, set the variables before doing the `if` conditions for cleaner code.

```python
def findPeakElement(self, nums: List[int]) -> int:
	n = len(nums)
	l, r = 0, n-1
	  
	while l <= r:
		m = l+(r-l)//2
		left = nums[m-1] if m-1>=0 else -inf
		right = nums[m+1] if m+1<n else -inf
	  
		# peak
		if left < nums[m] and nums[m] > right:
			return m
		elif left < nums[m] and nums[m] < right:
			l = m+1
		else: # descending
			r = m-1
```
