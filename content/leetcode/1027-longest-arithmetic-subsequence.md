---
type: leetcode
title: 1027. longest arithmetic subsequence
tags:
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-09-04
---

Given an array `nums` of integers, return _the length of the longest arithmetic subsequence in_ `nums`.

**Note** that:

- A **subsequence** is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.
- A sequence `seq` is arithmetic if `seq[i + 1] - seq[i]` are all the same value (for `0 <= i < seq.length - 1`).

## solutions

```python
def longestArithSeqLength(self, nums: List[int]) -> int:
	n = len(nums)
	# dp[(i, diff)] = longest subsequence ending at i with diff
	dp = {}
	res = 2
	
	for i in range(len(nums)-1):
		for j in range(i+1, len(nums)):
			diff = nums[j]-nums[i]
			if (i, diff) in dp:
				dp[(j, diff)] = dp[(i, diff)]+1
				res = max(res, dp[(j, diff)])
			else:
				dp[(j, diff)] = 2
	return res
```
