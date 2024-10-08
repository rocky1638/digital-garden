---
type: leetcode
title: 44. wildcard matching
tags:
  - recursion
  - memoization
aliases: 
parents:
  - "[[10-regular-expression-matching]]"
children: 
supports: 
enemies: 
date: 2024-09-24
updated: 2024-09-24
---

Given an input string (`s`) and a pattern (`p`), implement wildcard pattern matching with support for `'?'` and `'*'` where:

- `'?'` Matches any single character.
- `'*'` Matches any sequence of characters (including the empty sequence).

The matching should cover the **entire** input string (not partial).

## solution

```python
# O(2^(s+p)) without memoization, O(sp) with memoization
def isMatch(self, s: str, p: str) -> bool:
	"""
	considerations:
	- condense adjacent wildcards as they are redundant
	- for wildcards, three cases
	- match, and stay on wildcard
	- skip wildcard (don't advance string)
	- in the case where s is done but p is not,
	it's valid if all remaining p chars are wildcards
	"""
	  
	# adjacent wildcards (*) are redundant
	short_p = []
	for i in range(len(p)):
		if p[i] == "*" and i > 0 and p[i-1] == "*":
			continue
		short_p.append(p[i])
	p = "".join(short_p)
	  
	memo = {}
	def recurse(si, pi):
		if si == len(s) and pi == len(p):
			return True
		if si == len(s) or pi == len(p):
			if pi == len(p):
				return False
			if si == len(s):
				return all(c == "*" for c in p[pi:])
		if (si, pi) in memo:
			return memo[(si, pi)]
	  
			res = False
		if p[pi] == "*":
			# match (continue matching): si+1, pi
			# skip: si, pi+1
			res = recurse(si+1, pi) or recurse(si, pi+1)
		elif p[pi] == "?":
			res = recurse(si+1, pi+1)
		else: # normal char
			if p[pi] != s[si]:
				res = False
			else:
				res = recurse(si+1, pi+1)

		memo[(si, pi)] = res
		return res

	return recurse(0, 0)
```
