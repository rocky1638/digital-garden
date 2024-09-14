---
type: leetcode
title: 1004. max consecutive ones iii
tags:
  - sliding-window
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-29
---

Given a binary array `nums` and an integer `k`, return _the maximum number of consecutive_ `1`_'s in the array if you can flip at most_ `k` `0`'s.

## solution

Standard sliding window problem.

```python
def longestOnes(self, nums: List[int], k: int) -> int:
	num_zeroes = 0
	l = 0
	ans = 0

	for r in range(len(nums)):
		if nums[r] == 0:
			num_zeroes += 1
		  
		while num_zeroes > k:
			if nums[l] == 0:
				num_zeroes -= 1
			l += 1
		ans = max(ans, r-l+1)
	return ans
```
