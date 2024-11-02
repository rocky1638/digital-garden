---
type: leetcode
title: 474. ones and zeroes
tags:
  - recursion
  - memoization
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-17
updated: 2024-10-17
---

You are given an array of binary strings `strs` and two integers `m` and `n`.

Return _the size of the largest subset of `strs` such that there are **at most**_ `m` `0`_'s and_ `n` `1`_'s in the subset_.

A set `x` is a **subset** of a set `y` if all elements of `x` are also elements of `y`.

## solution

```python
def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
	memo = {}
	def recurse(idx, rem_zeroes, rem_ones):
		if idx == len(strs):
			return 0
		if rem_zeroes < 0 or rem_ones < 0:
			return 0
		  
		if (idx, rem_zeroes, rem_ones) in memo:
			return memo[(idx, rem_zeroes, rem_ones)]
		  
		best = 0
		# take if allowed
		if rem_zeroes >= blocks[idx][0] and rem_ones >= blocks[idx][1]:
			best = max(
				best,
				1+recurse(idx+1, rem_zeroes-blocks[idx][0], rem_ones-blocks[idx][1])
			)
		# skip
		best = max(best, recurse(idx+1, rem_zeroes, rem_ones))
		  
		memo[(idx, rem_zeroes, rem_ones)] = best
		return best
	  
	blocks = []
	for s in strs:
		c = Counter(s)
		blocks.append((c["0"], c["1"]))
	  
	return recurse(0, m, n)
```
