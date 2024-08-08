---
title: 33. search in rotated sorted array
created_at: 2022-11-21
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/search-in-rotated-sorted-array/
date: 2022-11-21
updated: 2024-07-31
tags:
  - binary-search
---

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return _the index of_ `target` _if it is in_ `nums`_, or_ `-1` _if it is not in_ `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

## solution

First binary search to find the pivot index. Then binary search on the correct side of the pivoted array _(rotated array is essentially two distinct sorted arrays)._

```python
def search(self, nums: List[int], target: int) -> int:
	"""
	1. Binary search to find the pivot index
	2. Binary search on the correct half
	"""
	def binary_search(arr, l, r, x):
		while l <= r:
			m = l+(r-l)//2
			if arr[m] == x:
				return m
			elif arr[m] < x:
				l = m+1
			else:
				r = m-1
		return -1
	  
	n = len(nums)
	l, r = 0, n-1
	pivot = None
	  
	while l <= r:
		m = l+(r-l)//2
	  
		# m is the largest value before drop, or end of array
		if m == n-1:
			pivot = -1
			break
		elif nums[m] > nums[m+1]:
			pivot = m+1
			break
		# in first half, move towards right
		elif nums[m] >= nums[0]:
			l = m+1
		else:
			r = m-1

	# unrotated
	if pivot == -1:
		return binary_search(nums, 0, len(nums)-1, target)
	  
	# target in right half
	if target < nums[0]:
		return binary_search(nums, pivot, len(nums)-1, target)
	return binary_search(nums, 0, pivot-1, target)
```
