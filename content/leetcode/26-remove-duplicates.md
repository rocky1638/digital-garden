---
type: leetcode
title: 26. remove duplicates
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-02
updated: 2024-09-10
---

Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each unique element appears only **once**. The **relative order** of the elements should be kept the **same**. Then return _the number of unique elements in_ `nums`.

Consider the number of unique elements of `nums` to be `k`, to get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of `nums` contain the unique elements in the order they were present in `nums` initially. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.

## solution

Because we don’t care about what ends up at the end of the array, just overwrite values.

```python
def removeDuplicates(self, nums: List[int]) -> int:
	res = len(nums)
	next_insert = 0
	i = 0
	  
	while i < len(nums):
		# put next unique value at next avail idx
		nums[next_insert] = nums[i]
		next_insert += 1
	  
		# advance i to next unique value
		i += 1
		while i < len(nums) and nums[i] == nums[i-1]:
			i += 1
			res -= 1
	return res
```
