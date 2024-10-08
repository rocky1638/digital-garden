---
type: leetcode
title: 523. continuous subarray sum
tags:
  - hashmap
  - prefix-sums
  - math
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-30
---


Given an integer array nums and an integer k, return `true` _if_ `nums` _has a **good subarray** or_ `false` _otherwise_.

A **good subarray** is a subarray where:

- its length is **at least two**, and
- the sum of the elements of the subarray is a multiple of `k`.

**Note** that:

- A **subarray** is a contiguous part of the array.
- An integer `x` is a multiple of `k` if there exists an integer `n` such that `x = n * k`. `0` is **always** a multiple of `k`.

## solution

```python
def checkSubarraySum(self, nums: List[int], k: int) -> bool:
	"""
	k = 6
	[0, 23, 25, 29, 35, 42]
	we can then make the prefix sums mod k
	[0, 5, 1, 5, 5, 0]
	  
	we can construct prefix, hashmap as we iterate right,
	look back to see if mod exists to the left

	if it does, the difference between two numbers of same mod k
	will be a multiple of k
	  
	length at least 2, so a single value with mod 0 won't work
	"""
  
	seen_mods = set()
	prefix_sums = [0]
	for num in nums:
		prefix_sums.append(prefix_sums[-1] + num)
		mod = prefix_sums[-1] % k
	  
		if mod in seen_mods:
			return True
		seen_mods.add(prefix_sums[-2] % k)
	return False
```
