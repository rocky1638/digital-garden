---
created_at: 2023-01-04
title: 875. koko eating bananas
type: leetcode
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/koko-eating-bananas/
date: 2023-01-04
updated: 2024-08-01
---

Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return _the minimum integer_ `k` _such that she can eat all the bananas within_ `h` _hours_.

## solution

We use binary search on the possible eating rates `k`, starting our bounds at 1 and the maximum sized pile of bananas.

```python
def minEatingSpeed(self, piles: List[int], h: int) -> int:
	def hoursToEat(k):
		return sum([math.ceil(b/k) for b in piles])

	l, r = 1, max(piles)
  
	while l <= r:
		m = l+(r-l)//2
		hours = hoursToEat(m)
	  
		if m == 1 and hours <= h:
			return m
		elif hours <= h and hoursToEat(m-1) > h:
			return m
		elif hours > h:
			l = m+1
		else:
			r = m-1
```

Here’s another option for writing the solution that’s a little simpler. See the article about the template for finding the “left bound” with binary search [here](https://leetcode.com/problems/koko-eating-bananas/solutions/769702/python-clear-explanation-powerful-ultimate-binary-search-template-solved-many-problems).

```python
def minEatingSpeed(piles: List[int], H: int) -> int:
	def feasible(speed) -> bool:
		return sum((pile - 1) / speed + 1 for pile in piles) <= H  # faster
	
	left, right = 1, max(piles)
	while left < right:
		mid = left  + (right - left) // 2
		if feasible(mid):
			right = mid
		else:
			left = mid + 1
	return left
```
