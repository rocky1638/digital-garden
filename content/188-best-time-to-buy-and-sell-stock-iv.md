---
type: leetcode
title: 188. best time to buy and sell stock iv
tags:
  - memoization
  - recursion
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-17
updated: 2024-10-17
---

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day, and an integer `k`.

Find the maximum profit you can achieve. You may complete at most `k` transactions: i.e. you may buy at most `k` times and sell at most `k` times.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

## solution

Recursion w/ memoization, although we have to maintain what our current state is, in the recursion. At any index, we can decide to take an action, or not.

If we take an action, it depends on our state. If we’re holding, we sell and gain the price of the current day. If we’re not holding, we buy and pay the cost of the current day.

```python
# O(nk)
def maxProfit(self, k: int, prices: List[int]) -> int:
	memo = {}
	def recurse(idx, actions, holding):
		if idx == len(prices) or actions == 2*k:
			return 0
		if (idx, actions, holding) in memo:
			return memo[(idx, actions, holding)]

		best = 0
		# take action
		if holding: # sell current holding stock
			best = max(
				best,
				prices[idx]+recurse(idx+1, actions+1, not holding)
			)
		else: # buy current stock
			best = max(
				best,
				-prices[idx]+recurse(idx+1, actions+1, not holding)
			)
		  
		# ...or skip
		best = max(best, recurse(idx+1, actions, holding))

		memo[(idx, actions, holding)] = best
		return best

	return recurse(0, 0, False)
```
