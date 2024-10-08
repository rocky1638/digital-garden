---
type: leetcode
title: 1590. make sum divisible by p
tags:
  - prefix-sums
  - hashmap
  - math
aliases: 
parents:
  - "[[523-continuous-subarray-sum]]"
children: 
supports: 
enemies: 
date: 2024-10-05
updated: 2024-10-05
---

Given an array of positive integers `nums`, remove the **smallest** subarray (possibly **empty**) such that the **sum** of the remaining elements is divisible by `p`. It is **not** allowed to remove the whole array.

Return _the length of the smallest subarray that you need to remove, or_ `-1` _if it's impossible_.

A **subarray** is defined as a contiguous block of elements in the array.

## solution

After discounting the brute force of computing every possible subarray, we realize that this problem follows the pattern of using a hashmap + prefix sums to efficiently find subarrays.

Some two changes are required here:

1. Instead of storing prefix sums, we need store the `mod` of the prefix sums relative to `p`.
	- We are looking for a subarray sum $S$ and total subarray sum $T$ such that $S\mod p = T\mod p$ (because removing this array would leave the rest array divisible by $p$.)
	- So, we look back in our hashmap for another prefix array whose sum is `mod(current_mod-total_mod)`. (This is just algebra).
	- We need to remember to consider the negative reflected mod as well!
2. Instead of counting valid subarrays, we want to find the shortest. So, instead of storing counts in the hashmap, we store the rightmost index of each prefix sum mod appearance.

```python
# O(n), space O(p)
def minSubarray(self, nums: List[int], p: int) -> int:
	"""
	[3,1,4,2] total = 10 = 4mod6
	prefix_mod_array = [3,4,2,4]
	
	we want to find the smallest subarray with
	sum mod 6 == total mod 6 (4, in this example)
	  
	current_mod - prev_mod = 4 or -2
	general: current_mod - prev_mod = total_mod or (total_mod - p)
	"""
	total = sum(nums)
	if p > total:
		return -1
	  
	total_mod = total % p
	if total_mod == 0:
		return 0
	  
	rightmost_mod_idx = {0: -1}
	res = inf
	  
	prefix_mod = 0
	for i, num in enumerate(nums):
		prefix_mod += num
		prefix_mod %= p
	  
		# use prefix sum mods to find subarray with sum mod p == target
		target = prefix_mod - total_mod
		if target in rightmost_mod_idx:
			res = min(res, i-rightmost_mod_idx[target])
	
		# add mod and negative reflection to hashmap
		rightmost_mod_idx[prefix_mod] = i
		rightmost_mod_idx[prefix_mod-p] = i
	  
	return -1 if res in {inf, len(nums)} else res
```
