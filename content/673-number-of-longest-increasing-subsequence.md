---
type: leetcode
title: 673. number of longest increasing subsequence
tags:
  - dp
aliases: 
parents:
  - "[[300-longest-increasing-subsequence]]"
children: 
supports: 
enemies: 
date: 2024-10-03
updated: 2024-10-03
---

Given an integer array `nums`, return _the number of longest increasing subsequences._

**Notice** that the sequence has to be **strictly** increasing.

## solution

We first start out fully with the solution for [[300-longest-increasing-subsequence]].

However, we need to realize that we need to keep another array `counts` that stores the number of ways that the LIS ending at $i$ can be reached.


> [!example]+
> Take the example `[1,2,4,3,5,4,7,2]`. Both the `5` and `4` before `7` have a LIS ending at them of length 4. However, the `5` actually has two ways to achieve this (`[1,2,4,5]` and `[1,2,3,5]`). When we then construct a LIS of length 5 ending at `7` , we need to count both of them.

```python
def findNumberOfLIS(self, nums: List[int]) -> int:
	# dp[i] = longest subsequence ending at i
	n = len(nums)
	dp = [1]*n
	counts = [1]*n
	max_len = 1
	  
	for i in range(n):
		for j in range(i):
			# each of these iterations is a unique subsequence
			# so we can count how many of each length we have
			if nums[j] < nums[i]:
				subseq_len = dp[j]+1
	  
				if subseq_len == dp[i]:
					counts[i] += counts[j]
				elif subseq_len > dp[i]:
					counts[i] = counts[j]
					dp[i] = subseq_len
					max_len = max(max_len, subseq_len)
	  
	res = 0
	for i in range(len(dp)):
		if dp[i] == max_len:
			res += counts[i]
	return res
```
