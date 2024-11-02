---
type: leetcode
title: 123. best time to buy and sell stock iii
tags:
  - recursion
  - memoization
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-09
updated: 2024-10-17
---

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete **at most two transactions**.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

## solutions

### top-down recursion w/ memoization (2d)

This was the most obvious logical approach for me. At each index, we can either buy at the current index and sell at any future index (which we all try), or skip the index.

```python
# O(n^2)
def maxProfit(self, prices: List[int]) -> int:
	memo = {}
	def recurse(idx, tx_completed):
		if idx == len(prices) or tx_completed == 2:
			return 0
		if (idx, tx_completed) in memo:
			return memo[(idx, tx_completed)]

		best = 0
		# buy on day idx, sell on any day afterwards
		for i in range(idx+1, len(prices)):
			if prices[i] > prices[idx]:
				best = max(
					best,
					prices[i]-prices[idx]+recurse(i+1, tx_completed+1)
				)
		  
		# don't buy on this day
		best = max(best, recurse(idx+1, tx_completed))
		  
		memo[(idx, tx_completed)] = best
		return best

	return recurse(0, 0)
```

### top-down recursion w/ memoization (3d)

Instead of trying every selling time for each index, we can keep track of our current state (holding/not holding). Then, our two options at each index are either:

1. Skip the index.
2. If we’re holding a stock, sell it and continue. If we’re not, buy it and continue.

```python
# O(n)
def maxProfit(self, prices: List[int]) -> int:
	memo = {}
	def recurse(idx, actions, holding):
		if idx == len(prices) or actions == 0:
			return 0
		if (idx, actions, holding) in memo:
			return memo[(idx, actions, holding)]
		  
		best = 0
		# if we aren't holding, buy stock
		if not holding:
			best = max(
				best,
				recurse(idx+1, actions-1, not holding) - prices[idx]
			)
		else: # if we are holding, sell stock and move to next index
			best = max(
				best,
				recurse(idx+1, actions-1, not holding) + prices[idx]
			)
		# skip
		best = max(best, recurse(idx+1, actions, holding))
		  
		memo[(idx, actions, holding)] = best
		return best

	return recurse(0, 4, False)
```

### clever one-pass simulation

There’s four values that we need to keep track of, and we can simulate through and keep the best possible for every value.

```python
# O(n)
def maxProfit(self, prices: List[int]) -> int:
	firstTransactionCost = prices[0]
	firstTransactionProfit = 0
	  
	mostMoneyInPocket = -prices[0]
	profitFromTwoTransactions = 0
	  
	for currentPrice in prices:
		firstTransactionCost = min(firstTransactionCost, currentPrice)
		firstTransactionProfit = max(
			firstTransactionProfit, currentPrice-firstTransactionCost
		)

		mostMoneyInPocket = max(
			mostMoneyInPocket, firstTransactionProfit-currentPrice
		)
		profitFromTwoTransactions = max(
			profitFromTwoTransactions, mostMoneyInPocket+currentPrice
		)

	return profitFromTwoTransactions
```
