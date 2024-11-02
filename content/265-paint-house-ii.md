---
type: leetcode
title: 265. paint house ii
tags:
  - recursion
  - memoization
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-10-13
---

There are a row of `n` houses, each house can be painted with one of the `k` colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by an `n x k` cost matrix costs.

- For example, `costs[0][0]` is the cost of painting house `0` with color `0`; `costs[1][2]` is the cost of painting house `1` with color `2`, and so on...

Return _the minimum cost to paint all houses_.

## solutions

### top-down recursion w/ memoization

The first intuition I had, we recurse with the current house being painted, cost so far, and the previous house’s color.

```python
# O(nk * some unbounded sum of costs)
def minCostII(self, costs: List[List[int]]) -> int:
	memo = {}
	def recurse(idx, acc, prev_color):
		if idx == len(costs):
			return acc
		if (idx, acc, prev_color) in memo:
			return memo[(idx, acc, prev_color)]

		best = inf
		for color, cost in enumerate(costs[idx]):
			if color == prev_color: continue
			best = min(best, recurse(idx+1, acc+cost, color))

		memo[(idx, acc, prev_color)] = best
		return best

	return recurse(0, 0, -1)
```

### optimized recursion w/ memoization

We realize that by having `acc` in the parameterization of the recursion, the 3D memoization space grows very large. Instead, we can skip out on an `acc` variable entirely, and use tail recursion to accumulate the total cost for a decision path (`total = cost + recurse(rest)`).

This improves our runtime to $O(nk^2)$ and passes on Leetcode.

```python
# O(nk * k)
def minCostII(self, costs: List[List[int]]) -> int:
	memo = {}
	def recurse(idx, prev_color):
		if idx == len(costs):
			return 0
		if (idx, prev_color) in memo:
			return memo[(idx, prev_color)]

		best = inf
		for color, cost in enumerate(costs[idx]):
			if color == prev_color: continue
			best = min(best, cost + recurse(idx+1, color))
		  
		memo[(idx, prev_color)] = best
		return best

	return recurse(0, -1)
```

### bottom-up dp

After understanding the previous solution, this one just requires a small mental tweak to reach. Instead of remembering the `prev_idx` in the recursion, we note that `dp[i][j]` represents the best cost we can achieve if we paint the `i`’th house with the `j`’th color.

```python
# O(nk*k)
def minCostII(self, costs: List[List[int]]) -> int:
	n = len(costs)
	k = len(costs[0])

	# dp[i][j] = minimum total cost if painting house i with color j
	dp = [[inf]*k for _ in range(n)]
	# base case, we just paint house 0 with every color and record cost
	for i in range(k):
		dp[0][i] = costs[0][i]

	for i in range(1, n):
		for j in range(k):
			dp[i][j] = costs[i][j]+min(dp[i-1][:j] + dp[i-1][j+1:])
	return min(dp[-1])
```
