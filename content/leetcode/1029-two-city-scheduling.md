---
type: leetcode
title: 1029. two city scheduling
date: 2022-11-17
updated: 2024-06-19
tags:
  - greedy
  - sorting
---

A company is planning to interview `2n` people. Given the array `costs` where `costs[i] = [aCosti, bCosti]`, the cost of flying the `ith` person to city `a` is `aCosti`, and the cost of flying the `ith` person to city `b` is `bCosti`.

Return _the minimum cost to fly every person to a city_ such that exactly `n` people arrive in each city.

## solution

We take a greedy approach to “filling up” the two cities.

The intuition is basically which person do we “gain” the most from when choosing to put them in city A or city B? The answer is that we gain the most from choosing someone when the difference in cost for the person is greatest _(alternatively, because we end up wasting the most money if we end up putting them in the more expensive city)_.

```python
def twoCitySchedCost(self, costs: List[List[int]]) -> int:
	n = len(costs) // 2
	costs.sort(key=lambda x: (abs(x[0]-x[1]), sum(x)), reverse=True)
	  
	num_flown = [0, 0]
	ans = 0
	  
	for c1, c2 in costs:
		if (num_flown[0] < n and c1 <= c2) or num_flown[1] == n:
			num_flown[0] += 1
			ans += c1
		elif (num_flown[1] < n and c2 <= c1) or num_flown[0] == n:
			num_flown[1] += 1
			ans += c2
	return ans
```
