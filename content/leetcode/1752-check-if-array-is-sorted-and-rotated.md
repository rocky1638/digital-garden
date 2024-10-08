---
type: leetcode
title: 1752. check if array is sorted and rotated
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-02
updated: 2024-09-02
---

Given an array `nums`, return `true` _if the array was originally sorted in non-decreasing order, then rotated **some** number of positions (including zero)_. Otherwise, return `false`.

There may be **duplicates** in the original array.

**Note:** An array `A` rotated by `x` positions results in an array `B` of the same length such that `A[i] == B[(i+x) % A.length]`, where `%` is the modulo operation.

## solutions

Just remember edge cases for monotone, single value.

```python
def check(self, nums: List[int]) -> bool:
	"""
	- iterate, adjacent elements must be non-decreasing (allow one decreasing)
	  
	- if we saw monotone, return True
	- if we saw no decreasing, nums[0] < nums[-1]
	- if we saw one decreasing, nums[0] >= nums[-1]
	  
	- special case monotone array (track if we see change at all?)
	"""
	if len(nums) == 1:
		return True
	  
	is_monotone = True
	num_decreasing = 0
	for v1, v2 in zip(nums[:-1], nums[1:]):
		if v1 != v2: is_monotone = False
		if v1 < v2:
			is_monotone = False
		elif v1 > v2:
			if num_decreasing > 0:
				return False
			num_decreasing += 1

	if is_monotone:
		return True
	return nums[0] < nums[-1] if num_decreasing == 0 else nums[0] >= nums[-1]
```
