---
type: leetcode
title: 161. is one edit distance
tags:
  - string
aliases: 
parents:
  - "[[72-edit-distance]]"
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-11
---

Given two strings `s` and `t`, return `true` if they are both one edit distance apart, otherwise return `false`.

A string `s` is said to be one distance apart from a string `t` if you can:

- Insert **exactly one** character into `s` to get `t`.
- Delete **exactly one** character from `s` to get `t`.
- Replace **exactly one** character of `s` with **a different character** to get `t`.

## solution

This problem is like a baby, non-recursive version of the harder [[72-edit-distance]] problem. Essentially, we take two pointers, and consider the two distinct cases:

1. The characters match. Advance both pointers.
2. The characters don’t match. We need to make an edit to make them match, and then continue.
	- If we use replacement, one of the characters is replaced to match, and we have to consider the next character in both strings.
	- If we use insertion/deletion, we only advance the pointer of one of the strings, instead of both. (See the original [[72-edit-distance]] for more intuition).

```python
def isOneEditDistance(self, s: str, t: str) -> bool:
	ps, pt = 0, 0
	while ps < len(s) or pt < len(t):
		# edge case when string is done reading
		if ps == len(s):
			return len(t[pt:]) == 1
		elif pt == len(t):
			return len(s[ps:]) == 1

		# characters match - continue
		if s[ps] == t[pt]:
			ps += 1
			pt += 1
		else:
			valid = False
			# replace (match current chars, rest must match)
			valid = valid or s[ps+1:] == t[pt+1:]
		  
			# insert (into s or t)
			# OR delete (s or t)
			return valid or s[ps+1:] == t[pt:] or s[ps:] == t[pt+1:]
```
