---
title: 518. coin change ii
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/coin-change-ii/
date: 2023-01-17
updated: 2024-05-29
tags:
  - dp
  - memoization
---

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the number of combinations that make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `0`.

You may assume that you have an infinite number of each kind of coin.

The answer is **guaranteed** to fit into a signed **32-bit** integer.

## top-down recursion with memoization

At each recursive step, we can either use the current coin, or move on to the next coin. Note that we go through the coins in order so that we don’t have differently ordered repeats _(we are only looking for combinations and not permutations)_.

```python
def change(self, amount: int, coins: List[int]) -> int:
	ans = 0
	cache = {}
	
	def recurse(coin_idx, subtotal):
		if subtotal == amount:
			return 1
		if subtotal > amount:
			return 0
		if coin_idx == len(coins):
			return 0
		if (coin_idx, subtotal) in cache:
			return cache[(coin_idx, subtotal)]
		
		# we either use the coin (first/again), or move on.
		cache[(coin_idx, subtotal)] = recurse(coin_idx, subtotal + coins[coin_idx]) + recurse(coin_idx + 1, subtotal)
		return cache[(coin_idx, subtotal)]
	
	return recurse(0, 0)
```

## 2d dynamic programming

We keep a 2D `dp` array that has each row as the length of the amount we’re trying to reach, and with number of rows equal to the coins that we’re considering.

`dp[i][j]` represents the number of ways that we can represent the subtotal `j` using the first `i` coins. Note that this is basically 0/1 knapsack.

### the recurrence relation

Assume that we have some set of coins $C_1, C_2 \dots C_{i-1}, C_i$, and are trying to find the number of ways to create an amount $n$.

The first realization is that for all of our combinations, we can partition the set of possible combinations on the ones that include at least one coin $C_x$, and combinations that include none of the coin $C_x$, where $x \in [0,i]$.

As such, if we want to know how to sum to $n$ using the coins $C_1 \dots C_i$, and if we assume that we already know how to sum to the values $[0,n-1]$ using the subset of coins $C_1 \dots C_{i-1}$, then, letting $N(n, i)$ be the number of combinations to sum to $n$ using coins $[0,i]$, we can use the recurrence relation below:

$$
\begin{align}
N(n,i) = N(n, i-1) + N(n-C_i, i)
\end{align}
$$

That is, the number of ways to create a sum of $n$ using the coins from $0$ to $i$ is the number of ways to create a sum of $n$ without using $C_i$, _plus_ as the number of ways to create $n-C_i$ using $C_i$.

```python
def change(self, amount: int, coins: List[int]) -> int:
	dp = [[0 for j in range(amount+1)] for i in range(len(coins))]
	
	for i in range(len(dp)):
		# there's always one way to
		# make 0 with any set of coins
		dp[i][0] = 1
	
	for i in range(len(dp)):
		for j in range(1, len(dp[0])):
			if i > 0:
				dp[i][j] += dp[i-1][j]
			if j-coins[i] >= 0:
				dp[i][j] += dp[i][j-coins[i]]

	return dp[-1][-1]
```

## memory optimization with 1d array

A standard optimization because we only ever look at the previous row, so we can just store at most two rows of the `dp` matrix in memory at once.

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0]*(amount+1)

        for i in range(1, len(coins)+1):
            nextDP = [0]*(amount+1)
            for j in range(amount+1):
                if j == 0:
                    # one way to make 0, don't take any coins
                    nextDP[j] = 1
                else:
                    # if we don't use the current coin
                    nextDP[j] = dp[j]
                    # if we do use the current coin
                    if coins[i-1] <= j:
                        nextDP[j] += nextDP[j-coins[i-1]]
            dp = nextDP

        return dp[-1]
```
