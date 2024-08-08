---
type: leetcode
title: 1249. minimum remove to make valid parentheses
tags:
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-10
updated: 2024-07-10
---

Given a string s of `'('` , `')'` and lowercase English characters.

Your task is to remove the minimum number of parentheses ( `'('` or `')'`, in any positions ) so that the resulting _parentheses string_ is valid and return **any** valid string.

Formally, a _parentheses string_ is valid if and only if:

- It is the empty string, contains only lowercase characters, or
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

## solution

We just iterate twice one way each through the string to find all unnecessary parentheses.

```python
def minRemoveToMakeValid(self, s: str) -> str:
	ls = list(s)

	# remove extra closing brackets
	op = 0
	for i, c in enumerate(ls):
		if c == "(":
			op += 1
		elif c == ")":
			if op == 0:
				ls[i] = None
			else:
				op -= 1

	# remove extra opening brackets
	op = 0
	for i in reversed(range(len(ls))):
		c = ls[i]
		if c == ")":
			op += 1
		elif c == "(":
			if op == 0:
				ls[i] = None
			else:
				op -= 1
	  
	return "".join([c for c in ls if c is not None])
```
