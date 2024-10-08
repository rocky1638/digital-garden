---
type: leetcode
title: 1043. partition array for maximum sum
tags:
  - backtracking
  - dp
  - memoization
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-14
updated: 2024-09-14
---

Given an integer array `arr`, partition the array into (contiguous) subarrays of length **at most** `k`. After partitioning, each subarray has their values changed to become the maximum value of that subarray.

Return _the largest sum of the given array after partitioning. Test cases are generated so that the answer fits in a **32-bit** integer._

## solutions

### brute-force backtracking

Basically at each index, we choose to add it to the current partition or stop and add it to the next partition.

```python
# O(2^n) - in the worst case, when k == n
def maxSumAfterPartitioning(self, arr: List[int], k: int) -> int:
	acc = 0
	res = 0

	def backtrack(idx):
		nonlocal acc, res
		if idx == len(arr):
			res = max(res, acc)

		partition_max = 0
		for i in range(idx, min(idx+k, len(arr))):
			partition_max = max(partition_max, arr[i])
			part_len = i-idx+1
			acc += partition_max*part_len
			backtrack(i+1)
			acc -= partition_max*part_len
	  
	backtrack(0)
	return res
```

### top-down recursion w/ memoization

We backtrack, but make sure to memoize the solutions for each subarray `arr[idx:]` in `memo[idx]`. Then, we can iterate through all possible partitions at an `idx`, and add those sums to the solution for the rest of the array.

This is basically DP but not.

```python
# O(nk)
def maxSumAfterPartitioning(self, arr: List[int], k: int) -> int:
	memo = {}
	def backtrack(idx):
		if idx == len(arr)-1:
			return arr[-1]
		  
		if idx in memo:
			return memo[idx]
		  
		best = 0
		partition_max = 0
		for i in range(idx, min(idx+k, len(arr))):
			partition_max = max(partition_max, arr[i])
			part_len = i-idx+1
			partition_sum = partition_max*part_len
			best = max(best, partition_sum + backtrack(i+1))

		memo[idx] = best
		return best
	  
	return backtrack(0)
```

### bottom-up dp

If we know the best solution for an array `arr[:i]`, then when we consider `arr[i]`, we can just check every possible partition size 1 to $k$ backwards, and see if we can get a better answer. It’s kind of like a more complicated [[70-climbing-stairs]].

```python
# O(nk)
def maxSumAfterPartitioning(self, arr: List[int], k: int) -> int:
	# dp[i] = best solution for array length i
	dp = [0]*(len(arr)+1)
	  
	for i in range(1, len(arr)+1):
		max_val = arr[i-1]
		for j in range(1, min(k, i)+1):
			max_val = max(max_val, arr[i-j])
			dp[i] = max(dp[i], dp[i-j] + max_val * j)
	return dp[-1]
```
