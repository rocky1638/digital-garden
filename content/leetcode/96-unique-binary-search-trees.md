---
type: leetcode
title: 96. unique binary search trees
tags:
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-07
updated: 2024-07-07
---

Given an integer `n`, return _the number of structurally unique **BST'**s (binary search trees) which has exactly_ `n` _nodes of unique values from_ `1` _to_ `n`.

## solution

I initially tried to solve this by recursing down all of the possible trees, keeping track of the current node and which nodes we’ve already used. However, there’s two intuitions that need to be made.

1. When creating a BST with an initial consecutive sequence of numbers from 1 to $n$, we know that when we pick a root node, we always split the nodes into two pieces (and the recursions don’t need to care about the half that they can’t use anymore).
2. With this intuition, we realize that we’re always working with a consecutive subsequence of the original 1 to $n$ range. So, we don’t actually care about what the numbers are, but just how long the subsequence is. This lends itself to realizing that there is repeated work, and then to dynamic programming.
3. We realize that to calculate the number of ways to arrange a BST with values $[1,n]$, we pick any root node $x \in [1,n]$, and then multiply the number of ways to arrange a BST of length $x-1$ (the left half) and $n-x$ (the right half). If we work up in dynamic programming, we’ll already have these values cached.

```python
def numTrees(self, n: int) -> int:
	# dp[i] = number of BST configurations
	# with sequence of i numbers
	dp = [0]*(n+1)
	dp[0] = 1
	dp[1] = 1
	  
	# build up answers for number of BSTs with sequence length i
	for i in range(2, n+1):
		# choose each breakpoint as root in BST
		# this is equal to the combination of ways to
		# make the left and right subtrees
		for j in range(1, i+1):
			dp[i] += dp[j-1] * dp[i-j]

	return dp[-1]
```
