---
type: leetcode
title: "115. distinct subsequences"
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-05-16
---

Given two strings s and t, return _the number of distinct_ **_subsequences_** _of_ s _which equals_ t.

The test cases are generated so that the answer fits on a 32-bit signed integer.

## solutions

### recursion w/ memoization

We recurse with two pointers. If the two characters are the same, we can decide to match the characters (advance both pointers), or we can decide to not use the match, and advance the pointer in our source string $S$.

If the characters don’t match, we must advance our pointer for the source string $S$.

```python
def numDistinct(self, s: str, t: str) -> int:
	memo = {}

	def recurse(si, ti):
		# finished constructing t
		if ti == len(t):
			return 1
		# reached end of s without constructing t
		if si == len(s):
			return 0
	
		if (si, ti) in memo:
			return memo[(si, ti)]
	
		ans = 0
		if s[si] == t[ti]:
			# match and move forward
			ans += recurse(si+1, ti+1)
			# skip the match, or no match
			ans += recurse(si+1, ti)
	
		memo[(si, ti)] = ans
		return memo[(si, ti)]
	
	return recurse(0, 0)
```

### dynamic programming

To convert the above solution to a bottom-up, we start by reasoning about what happens when either of the strings are empty.

> Note that `dp[s][t]` is the number of ways `S[:s]` can be used to construct `S[:t]`.

1. When the source string $S$ is empty, we always have an answer of 0, because we can’t make any target strings using an empty source string (except when $T$ is also an empty string).
2. When the target string $T$ is empty, we always have an answer of 1.

Now, for the recurrence relation, we can just flip the recurrence relations that we used in the top-down approach above.

From `recurse(si+1, ti+1)`, we get `dp[i][j] = dp[i-1][j-1]`, and from `recurse(si+1, ti)`, we get `dp[i][j] = dp[i][j-1]`.

```python
def numDistinct(self, s: str, t: str) -> int:
	dp = [[0 for i in range(len(s)+1)] for j in range(len(t)+1)]

	for j in range(len(s)+1):
		dp[0][j] = 1
	
	for i in range(1, len(t)+1):
		for j in range(1, len(s)+1):
			if t[i-1] == s[j-1]:
				dp[i][j] += dp[i-1][j-1]
			dp[i][j] += dp[i][j-1]
	
	return dp[-1][-1]
```
