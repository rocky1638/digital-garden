---
type: leetcode
title: 80. remove duplicates from sorted array ii
tags:
  - two-pointer
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-10
updated: 2024-09-10
---

Given an integer array `nums` sorted in **non-decreasing order**, remove some duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each unique element appears **at most twice**. The **relative order** of the elements should be kept the **same**.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the **first part** of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.

Return `k` _after placing the final result in the first_ `k` _slots of_ `nums`.

Do **not** allocate extra space for another array. You must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

## solution

Heavily inspired by [[26-remove-duplicates]]. We keep track of the next index to overwrite. Tricky part is also keeping track of counts as we iterate through the array.

```python
def removeDuplicates(self, nums: List[int]) -> int:
	prev = nums[0]
	count = 1
	next_valid = 1
	p = 1
	  
	while p < len(nums):
		# update counts
		if nums[p] == nums[p-1]:
			count += 1
		else:
			prev = nums[p]
			count = 1
		  
		# duplicate
		if count > 2:
			p += 1
		else:
			if p != next_valid:
				nums[next_valid] = nums[p]
			p += 1
			next_valid += 1
	  
	num_removed = p - next_valid
	return len(nums)-num_removed
```
