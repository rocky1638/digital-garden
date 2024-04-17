---
type: leetcode
title: 122. best time to buy and sell stock ii
tags:
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-04-12
---

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return _the **maximum** profit you can achieve_.

## solution

This one’s pretty simple. Because we have no restriction on buying and selling, we can just always take a buy/sell for two consecutive days if it nets us a positive profit.

```python
def maxProfit(self, prices: List[int]) -> int:
	profit = 0
	for p1, p2 in zip(prices[:-1], prices[1:]):
		profit += max(0, p2-p1)
	return profit
```
