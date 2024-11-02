---
type: leetcode
title: 1497. check if array pairs are divisible by k
tags:
  - counting-sort
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-10-17
---

Given an array of integers `arr` of even length `n` and an integer `k`.

We want to divide the array into exactly `n / 2` pairs such that the sum of each pair is divisible by `k`.

Return `true` _If you can find a way to do that or_ `false` _otherwise_.

## solution

I initially thought about enumerating every possible pair combination, but that would be very slow.

The key intuition is that for two numbers $x$ and $y$ to sum up to a value divisible by $k$, we need to satisfy the condition $x\mod k + y \mod k = k$. So, we just need there to be the same number of values in the array that are mod complements of each other.

Remember to consider the edge cases of mod values of 0 and $k/2$.

```python
def canArrange(self, arr: List[int], k: int) -> bool:
	"""
	precompute { mod_k: count of vals }
	  
	for any mod, mod1 + mod2 == k (adding will be divisible)
	# we can't do mod1 == mod2 because that's subtracting
	"""
	  
	d = Counter()
	for num in arr:
		d[num%k] += 1
	  
	# to handle num mod k == 0 case
	d[k] = d[0]
	for key in d:
		if d[key] != d[k-key]:
			return False
		# if the mod == k/2, we're gonna have
		# to take both values from here, so must be even
		if key == k-key and d[key] & 1:
			return False
	return True
```
