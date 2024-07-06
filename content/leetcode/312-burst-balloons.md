---
type: leetcode
title: 312. burst balloons
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-05-28
---

You are given `n` balloons, indexed from `0` to `n - 1`. Each balloon is painted with a number on it represented by an array `nums`. You are asked to burst all the balloons.

If you burst the `ith` balloon, you will get `nums[i - 1] * nums[i] * nums[i + 1]` coins. If `i - 1` or `i + 1` goes out of bounds of the array, then treat it as if there is a balloon with a `1` painted on it.

Return _the maximum coins you can collect by bursting the balloons wisely_.

## solution

### brute force

From the outset, it’s easy to imagine a backtracking solution where we enumerate every possible path of balloon pops.

Even with caching, this means there are $2^n$ possibilities of states, leading to $O(n2^n)$.

### optimized

The main idea here comes from a trick and a shift in thinking. If we recurse by choosing which balloon to remove, we will end up with $2^n$ different subsequences.

However, if we choose which balloon to pop last, we can safely recurse on the left and right subarrays, because we know that in those recursions, the two subarrays won’t interact with each other!

This way, we only ever have to consider states of subarrays and not subsequences, leading to $n^2$ possible states.

```python
def maxCoins(self, nums: List[int]) -> int:
	nums = [1] + nums + [1]

	@lru_cache(None)
	def dp(l, r):
		if l > r:
			return 0
		if l == r:
			return nums[l-1] * nums[l] * nums[l+1]
		return max(
			dp(l, m-1) + dp(m+1, r) + nums[l-1] * nums[m] * nums[r+1] for m in range(l, r+1))
	return dp(1, len(nums) - 2)
```

## references

- https://www.youtube.com/watch?v=VFskby7lUbw
