---
type: leetcode
title: 410. split array largest sum
tags:
  - memoization
  - recursion
  - binary-search
  - dp
  - prefix-sums
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-22
updated: 2024-08-23
---

Given an integer array `nums` and an integer `k`, split `nums` into `k` non-empty subarrays such that the largest sum of any subarray is **minimized**.

Return _the minimized largest sum of the split_.

A **subarray** is a contiguous part of the array.

## solutions

### recursion w/ memoization

```python
def splitArray(self, nums: List[int], k: int) -> int:
	n = len(nums)
	prefix_sum = [0] + list(itertools.accumulate(nums))
	memo = {}
	  
	def recurse(idx, subarrays_remaining):
		"""
		Return the biggest split value for nums[idx:] given
		split into subarrays_remaining subarrays
		"""
		if (idx, subarrays_remaining) in memo:
			return memo[(idx, subarrays_remaining)]
		  
		# if no more splitting, just return sum of remaining array
		if subarrays_remaining == 1:
			return prefix_sum[n]-prefix_sum[idx]

		best = inf
		# for each possible split idx, recurse and
		# take the best possible answer
		for i in range(idx, n-subarrays_remaining+1):
			left_split_sum = prefix_sum[i+1] - prefix_sum[idx]
		  
			best_with_split = max(
				left_split_sum,
				recurse(i+1, subarrays_remaining-1)
			)
		  
			best = min(best, best_with_split)
		  
			# break early if our left split is already
			# worse than our best total split
			if left_split_sum >= best:
				break
		  
		memo[(idx, subarrays_remaining)] = best
		return best
	  
	return recurse(0, k)
```

### binary search

Instead of recursing through every possible valid state, we can actually just binary search for the best answer, and then do a linear scan per value to check if that value is valid, kind of like [[875-koko-eating-bananas]].
