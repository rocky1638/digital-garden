---
type: leetcode
title: 2419. longest subarray with maximum bitwise and
tags:
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-18
updated: 2024-09-18
---

You are given an integer array `nums` of size `n`.

Consider a **non-empty** subarray from `nums` that has the **maximum** possible **bitwise AND**.

- In other words, let `k` be the maximum value of the bitwise AND of **any** subarray of `nums`. Then, only subarrays with a bitwise AND equal to `k` should be considered.

Return _the length of the **longest** such subarray_.

The bitwise AND of an array is the bitwise AND of all the numbers in it.

A **subarray** is a contiguous sequence of elements within an array.

## solution

The only intuition required here is that the bitwise AND of two numbers will always be $\le$ the bigger of the two values.

So, this question is really just asking for the longest block of the maximum value in the array (because the biggest bitwise AND will always consist of just the maximum value of the array).

```python
def longestSubarray(self, nums: List[int]) -> int:
	res = 1
	best = nums[0]
	prev = nums[0]
	count = 1
	  
	for num in nums[1:]:
		if num == prev:
			count += 1
	  
			if num == best:
				res = max(res, count)

		else:
			if num > best:
				best = num
				res = 1
			prev = num
			count = 1

	return res
```
