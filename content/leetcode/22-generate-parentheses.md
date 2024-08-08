---
title: 22. generate parentheses
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/generate-parentheses/
date: 2022-12-09
updated: 2024-08-03
tags:
  - backtracking
  - string
---

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

## solution

This is a classic backtracking problem, very similar to [[46-permutations]].

```python
def generateParenthesis(self, n: int) -> List[str]:
	ans = []
	def recurse(o, c, acc):
		if o == c and o == n:
			ans.append(acc)
			return
	  
		if o == c:
			recurse(o+1, c, acc+"(")
		elif o > c:
			if o < n:
				recurse(o+1, c, acc+"(")
			recurse(o, c+1, acc+")")

	recurse(0, 0, "")
	return ans
```
