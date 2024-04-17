---
type: leetcode
title: 2466. count ways to build good strings
tags:
  - backtracking
  - memoization
  - dfs
aliases: 
parents:
  - "[[322-coin-change]]"
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-04-17
---

Given the integers `zero`, `one`, `low`, and `high`, we can construct a string by starting with an empty string, and then at each step perform either of the following:

- Append the character `'0'` `zero` times.
- Append the character `'1'` `one` times.

This can be performed any number of times.

A **good** string is a string constructed by the above process having a **length** between `low` and `high` (**inclusive**).

Return _the number of **different** good strings that can be constructed satisfying these properties._ Since the answer can be large, return it **modulo** `109 + 7`.

## solutions

### recursion with memoization

```python
def countGoodStrings(self, low: int, high: int, zero: int, one: int):
	memo = {}

	def recurse(length):
		if length > high:
			return 0
	  
		if length in memo:
			return memo[length]
	  
		ret = recurse(length+zero) + recurse(length+one)
	  
		if length >= low:
			ret += 1

		memo[length] = ret % (10**9+7)
		return memo[length]

	return recurse(0)
```

### dynamic programming

```python
def countGoodStrings(self, low: int, high: int, zero: int, one: int):
	dp = [0] * (high+1)
	dp[0] = 1 # seed value
	ans = 0

	for i in range(1, high+1):
		val = 0
		if i - zero >= 0:
			val += dp[i-zero]
		if i - one >= 0:
			val += dp[i-one]
	  
		dp[i] = val
		if low <= i <= high:
			ans += val
			ans %= (10**9+7)

	return ans
```
