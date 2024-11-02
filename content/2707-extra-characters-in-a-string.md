---
type: leetcode
title: 2707. extra characters in a string
tags:
  - recursion
  - memoization
  - dp
  - trie
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-23
updated: 2024-10-23
---

You are given a **0-indexed** string `s` and a dictionary of words `dictionary`. You have to break `s` into one or more **non-overlapping** substrings such that each substring is present in `dictionary`. There may be some **extra characters** in `s` which are not present in any of the substrings.

Return _the **minimum** number of extra characters left over if you break up_ `s` _optimally._

## solution

Basic recursion and memoization. If we used a trie, we could get this down to $O(n^2)$.

```python
# O(n^3)
def minExtraChar(self, s: str, dictionary: List[str]) -> int:
	dict_set = set(dictionary)
	memo = {}

	# O(n) instances
	def recurse(idx):
		if idx == len(s):
			return 0
	  
		if idx in memo:
			return memo[idx]

		best = inf

		# skip
		best = min(best, 1 + recurse(idx+1))

		# take all possibilities
		for i in range(idx, len(s)): # O(n)
			substr = s[idx:i+1] # O(n) -> trie could make this O(1)
			if substr in dict_set:
				best = min(best, recurse(i+1))

		memo[idx] = best
		return best

	return recurse(0)
```
