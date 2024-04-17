---
title: 322. coin change
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/coin-change/
date: 2022-11-22
updated: 2024-04-17
tags:
  - dp
---

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the fewest number of coins that you need to make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

## solution

Use dynamic programming to keep track of the minimum number of coins required to make each `amount` from 0 to `amount`.

Let $d_i$ be the value of the `dp` array at `i`. Let $C$ be the set of coin values, and $c_i$ be the value of the coin at index $i$ in the `coins` array. Then, our recursive relation is as follows:

$$
M_i=
\begin{cases}
1 \text{ if } i \in C, \\
\min(d_{i-c_i}) \forall c_i \in C \text{ otherwise}
\end{cases}
$$

```python
def coinChange(self, coins: List[int], amount: int) -> int:
	dp = [0]*(amount+1)
	
	for i in range(1, amount+1):
		m = float("inf")
		for coin in coins:
			if i-coin >= 0 and dp[i-coin] >= 0:
				m = min(m, dp[i-coin]+1)
			dp[i] = m
	
	return dp[-1] if dp[-1] != float("inf") else -1
```
