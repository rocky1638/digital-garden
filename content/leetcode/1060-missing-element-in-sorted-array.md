---
type: leetcode
title: 1060. missing element in sorted array
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-11
updated: 2024-09-11
---

Given an integer array `nums` which is sorted in **ascending order** and all of its elements are **unique** and given also an integer `k`, return the `kth` missing number starting from the leftmost number of the array.

## solution

First of all, the number of numbers missing from some array index `m` is equal to `nums[m]-nums[0]-m`.

We can `bisect_left` on `k` to find the first index where `num_missing` is greater than or equal to `k`.

Then the calculation at the end goes as follows:

1. `nums[0]+k` is equal to the kth missing element, if there were no other values in `nums` except for the first value.
2. `l` represents how many values in the range from `[nums[0], nums[0]+k]` already exist in the array. This means that we have to push further ahead to find our kth element.
3. We subtract 1 because the `bisect_left` ends `l` at the first index that has $\ge$ `k` missing elements, meaning that the element at `nums[l]` does not interfere with our kth missing element, so we ignore it and move `l` back by 1.

```python
def missingElement(self, nums: List[int], k: int) -> int:
	# bisect_left
	l, r = 0, len(nums)
	while l < r:
		m = (l+r)//2
		num_missing = nums[m]-nums[0]-m
		if num_missing < k:
			l = m+1
		else:
			r = m
	# base
	# + num_missing
	# + offset
	return nums[0] + k + l - 1
```
