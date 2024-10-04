---
type: leetcode
title: 416. partition equal subset sum
tags:
  - recursion
  - memoization
  - dp
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/partition-equal-subset-sum/
date: 2022-11-22
updated: 2024-09-28
---

Given an integer array `nums`, return `true` _if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or_ `false` _otherwise_.

## solutions

### recursion w/ memoization

```python
def canPartition(self, nums: List[int]) -> bool:
	s = sum(nums)
	if s & 1:
		return False
	  
	target = s // 2
	memo = {}
	def recurse(idx, acc):
		nonlocal target
		if acc == target:
			return True
		if idx == len(nums) or acc > target:
			return False
		if (idx, acc) in memo:
			return memo[(idx, acc)]

		res = False
		# take
		res |= recurse(idx+1, acc+nums[idx])
		# skip
		res |= recurse(idx+1, acc)
		  
		memo[(idx, acc)] = res
		return res

	return recurse(0, 0)
```

### dp

- to see if the array can be divided into two equal subsets, we just need to make sure that a subset of the array can sum to half of the total sum of the array.
- to do this, we can do it either top-down or bottom-up with [[dynamic-programming]].
- when doing top-down, we can just use [[recursion]] with [[memoization]].
- with bottom-up, this problem is very similar to the knapsack problem.
	- at each value in `nums`, we can choose to either use it or not use it.
	- working up the possible `sum` values from 0 to half of the total sum, we know that the sum of `j` can be created using the numbers in `nums[:i]` with two cases: _(`dp[i][j]`, where `j` is the current sum)_
		- not using the current value `nums[i]`, we can just look at `dp[i-1][j]`.
		- using the current value, we look at `dp[i-1][j-nums[i]]` (only if `nums[i]` is $\leq j$.
	- for my actual implementation, i just store the previous row of the `dp` instead of everything, for memory purposes.

```python
def canPartition(self, nums: List[int]) -> bool:
	s = sum(nums)
	if s & 1:
		return False
	target = s // 2
	  
	# sum of 0 is trivially doable
	dp = [[True]+[False]*target for _ in range(len(nums)+1)]
	  
	for i in range(1, len(nums)+1):
		for j in range(1, target+1):
			skip = dp[i-1][j]
	  
			take = False
			if j >= nums[i-1]:
				take = dp[i-1][j-nums[i-1]]
	  
			dp[i][j] = skip or take

	return dp[-1][-1]
```

## references

- https://en.wikipedia.org/wiki/Knapsack_problem
