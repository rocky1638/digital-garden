---
type: leetcode
title: 10. regular expression matching
tags:
  - memoization
  - dp
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-03
---

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

- `'.'` Matches any single character.​​​​
- `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

## solution

The idea here at it’s route is pretty straightforward, but there’s a lot of edge cases to consider. Essentially, we can break it down into two types of rules in the regex pattern.

1. Includes wildcard, of the form `[a-z]*` or `.*`.
2. Doesn’t include wildcard.

If the current rule doesn’t include a wildcard, just check for a match. If no match, return false. If it is a wildcard, we can match the current rule any number of times. However, for the sake of the recursion, we try to match either 0 times (and then recurse with the next rule), or one time (and then keep recursing with the same rule, to potentially capture multiple matches).

```python
def isMatch(self, s: str, p: str) -> bool:
	# (char, isWildcard)
	grouped_pattern = []
	i = 0
	while i < len(p):
		if i+1 == len(p):
			grouped_pattern.append((p[i], False))
		elif p[i+1] == "*":
			grouped_pattern.append((p[i], True))
			i+=1
		else:
			grouped_pattern.append((p[i], False))
		i+=1

	memo = {}
	def recurse(sp, pp):
		if (sp, pp) in memo:
			return memo[(sp, pp)]
	  
		if sp == len(s) and pp == len(grouped_pattern):
			return True

		ans = None
		if pp < len(grouped_pattern):
			char, is_wildcard = grouped_pattern[pp]
	  
			# for trailing wildcard groups
			if sp == len(s):
				if is_wildcard:
					ans = recurse(sp, pp+1)
				else:
					ans = False
	  
			# is wildcard
			elif is_wildcard:
				# empty match
				success = recurse(sp, pp+1)
				if sp < len(s) and (s[sp] == char or char == "."):
					# match once and recurse to try to keep matching
					success = success or recurse(sp+1, pp)
				ans = success

			else:
				if s[sp] == char or char == ".":
					ans = recurse(sp+1, pp+1)
				else:
					ans = False
	  
		memo[(sp, pp)] = ans
		return ans

	return recurse(0, 0)
```
