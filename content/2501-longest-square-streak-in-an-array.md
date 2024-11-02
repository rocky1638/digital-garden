---
type: leetcode
title: 2501. longest square streak in an array
tags:
  - dp
  - hashmap
  - sorting
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-10-30
---

You are given an integer array `nums`. A subsequence of `nums` is called a **square streak** if:

- The length of the subsequence is at least `2`, and
- **after** sorting the subsequence, each element (except the first element) is the **square** of the previous number.

Return _the length of the **longest square streak** in_ `nums`_, or return_ `-1` _if there is no **square streak**._

A **subsequence** is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

## solution

```python
def longestSquareStreak(self, nums: List[int]) -> int:
	n = len(nums)
	nums.sort()
	  
	# dp[i] is longest valid subsequence ending at i
	dp = [1]*n
	  
	# next val in sequence, idx of prev val
	next_vals = {nums[0]**2: 0}
	  
	for i in range(1, len(nums)):
		if nums[i] in next_vals:
			dp[i] = max(dp[i], dp[next_vals[nums[i]]]+1)
		next_vals[nums[i]**2] = i

	best = max(dp)
	return best if best > 1 else -1
```
