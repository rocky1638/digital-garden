---
type: leetcode
title: 283. move zeroes
date: 2022-12-21
updated: 2024-08-29
tags:
  - two-pointer
---

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

## solution

We use a two pointers strategy to swap zeroes to the back of the array. Keep track of where the leftmost zero is, and where the leftmost nonzero that is *to the right* of a zero is.

```python
def moveZeroes(self, nums: List[int]) -> None:
	n = len(nums)
	z = 0
	  
	# advance z to first 0
	while z < n and nums[z] != 0:
		z += 1
	  
	v = z
	# advance v to first non-0
	while v < n and nums[v] == 0:
		v += 1
	  
	while z < n and v < n:
		nums[z], nums[v] = nums[v], nums[z]
	  
		while z < n and nums[z] != 0:
			z += 1
		while v < n and nums[v] == 0:
			v += 1
```
