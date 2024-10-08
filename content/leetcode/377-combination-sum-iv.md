---
type: leetcode
title: 377. combination sum iv
tags:
  - recursion
  - memoization
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-06
updated: 2024-10-06
---

Given an array of **distinct** integers `nums` and a target integer `target`, return _the number of possible combinations that add up to_ `target`.

The test cases are generated so that the answer can fit in a **32-bit** integer.

## solutions

### recursion w/ memoization

```python
def combinationSum4(self, nums: List[int], target: int) -> int:
	memo = {}
	def recurse(remaining):
		if remaining == 0:
			return 1
		if remaining < 0:
			return 0

		if remaining in memo:
			return memo[remaining]

		ways = 0
		for num in nums:
			ways += recurse(remaining-num)
		memo[remaining] = ways
		return ways
	  
	return recurse(target)
```
