---
type: leetcode
title: 1216. valid palindrome iii
tags:
  - recursion
  - memoization
  - dp
aliases: 
parents: 
children: 
supports:
  - "[[pal"
enemies: 
date: 2024-09-01
updated: 2024-09-01
---

Given a string `s` and an integer `k`, return `true` if `s` is a `k`**-palindrome**.

A string is `k`**-palindrome** if it can be transformed into a palindrome by removing at most `k` characters from it.

## solutions

### top-down w/ memoization

At each step, we continue if the end characters are the same, or skip one of them and decrement our available removals.

```python
def isValidPalindrome(self, s: str, k: int) -> bool:
	memo = {}

	def recurse(l, r, removals):
		if (l, r, removals) in memo:
			return memo[(l, r, removals)]
	  
		if removals < 0:
			return False
	  
		# success case
		if l==r or (r-l==1 and s[r]==s[l]):
			return removals >= 0
	  
		res = None
		if s[l] == s[r]:
			res = recurse(l+1, r-1, removals)
		else:
			res = (
				recurse(l+1, r, removals-1)
				or recurse(l, r-1, removals-1)
			)
		memo[(l, r, removals)] = res
		return res
	  
	return recurse(0, len(s)-1, k)
```

### iterative dp

Translating the top-down solution above to bottom-up DP is generally not too hard. However, there’s a couple “aha” moments.

1. We can index by `(l, r)`, and store the number of removals it takes to reach a palindrome for each substring.
2. At each DP step, we will need to reference strings of smaller length, so these will need to be solved already. So, iterate through the possible substrings by length, increasing.

```python
def isValidPalindrome(self, s: str, k: int) -> bool:
	# dp[(l, r)]
	# number of removals required to make s[l:r+1] palindrome
	dp = defaultdict(int)
	  
	# iterate by lengths (all length 1 strings, all length 2 strings...)
	for length in range(1, len(s)+1):
		for l in range(0, len(s)-length+1):
			r = l+length-1
	  
			# base cases
			if length == 1:
				dp[(l, r)] = 0
			elif length == 2 and s[l] == s[r]:
				dp[(l, r)] == 0

			else:
				if s[l]==s[r]:
					dp[(l, r)] = dp[(l+1, r-1)]
				else:
					dp[(l, r)] = min(dp[(l+1, r)], dp[(l, r-1)]) + 1
	return dp[(0, len(s)-1)] <= k
```
