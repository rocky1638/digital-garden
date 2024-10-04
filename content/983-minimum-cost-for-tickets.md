---
type: leetcode
title: 983. minimum cost for tickets
tags:
  - recursion
  - memoization
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-28
updated: 2024-09-28
---

You have planned some train traveling one year in advance. The days of the year in which you will travel are given as an integer array `days`. Each day is an integer from `1` to `365`.

Train tickets are sold in **three different ways**:

- a **1-day** pass is sold for `costs[0]` dollars,
- a **7-day** pass is sold for `costs[1]` dollars, and
- a **30-day** pass is sold for `costs[2]` dollars.

The passes allow that many days of consecutive travel.

- For example, if we get a **7-day** pass on day `2`, then we can travel for `7` days: `2`, `3`, `4`, `5`, `6`, `7`, and `8`.

Return _the minimum number of dollars you need to travel every day in the given list of days_.

## solutions

### recursion w/ memoization

This was my initial idea with recursion/memoization. Backtracking, and skip if we’ve already paid for a day.

```python
# O(3^n) without memoization, O(n) with memoization
def mincostTickets(self, days: List[int], costs: List[int]) -> int:
	memo = {}
	def recurse(idx, paid_until):
		if idx == len(days):
			return 0

		if (idx, paid_until) in memo:
			return memo[(idx, paid_until)]

		min_cost = inf
		# prev payment covers today already
		if paid_until >= days[idx]:
			min_cost = recurse(idx+1, paid_until)
		# we must pay again today
		else:
			# take 1-day
			min_cost = min(
				recurse(idx+1, days[idx])+costs[0],
				min_cost
			)
			# take 7-day
			min_cost = min(
				recurse(idx+1, days[idx]+6)+costs[1],
				min_cost
			)
			# take 30-day
			min_cost = min(
				recurse(idx+1, days[idx]+29)+costs[2],
				min_cost
			)

		memo[(idx, paid_until)] = min_cost
		return min_cost
	  
	return recurse(0, 0)
```

### bottom-up dp

Similar to [[70-climbing-stairs]].

We don’t actually need to care about how far our pass extends in the future, as we can just tabulate while looking backwards.

To reach any day $d$, we can either buy a 1-day pass from yesterday, a 7-day pass from last week, or a 30-day pass from last month. This is represented in the `c1`, `c2`, and `c3` calculations. This is sort of a reversal of thinking from the top-down approach (which makes sense lol).

```python
def mincostTickets(self, days: List[int], costs: List[int]) -> int:
	dp = [0]*(days[-1]+1)
	  
	for i in range(1, days[-1]+1):
		if i in days:
			c1 = dp[i-1]+costs[0]
			c2 = dp[max(0, i-7)]+costs[1]
			c3 = dp[max(0, i-30)]+costs[2]
			dp[i] = min(c1, c2, c3)
		else:
			# we don't need to pay for this
			# day, so don't purchase anything
			dp[i] = dp[i-1]
	return dp[-1]
```
