---
type: leetcode
title: 1593. split a string into the max number of unique substrings
tags:
  - recursion
  - backtracking
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-22
updated: 2024-10-22
---

Given a string `s`, return _the maximum number of unique substrings that the given string can be split into_.

You can split string `s` into any list of **non-empty substrings**, where the concatenation of the substrings forms the original string. However, you must split the substrings such that all of them are **unique**.

A **substring** is a contiguous sequence of characters within a string.

## solution

We basically just enumerate all the valid possible splits using recursion. Note that we can’t memoize because `seen` is global and not in the recursion parameters. Even if we did memoize, we wouldn’t really get a speed up with it because seeing the same `(idx, splits, seen)` between two branches would be pretty rare (almost impossible?).

```python
# O(n2^n)
def maxUniqueSplit(self, s: str) -> int:
	seen = set()
	  
	def recurse(idx, splits):
		if idx == len(s):
			return splits

		best = 0
		for i in range(idx, len(s)):
			substr = s[idx:i+1]
			if substr in seen:
				continue
			seen.add(substr)
			best = max(best, recurse(i+1, splits+1))
			seen.remove(substr)
		return best
	  
	return recurse(0, 0)
```
