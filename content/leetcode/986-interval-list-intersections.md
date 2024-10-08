---
type: leetcode
title: 986. interval list intersections
tags:
  - intervals
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-10
updated: 2024-08-10
---

You are given two lists of closed intervals, `firstList` and `secondList`, where `firstList[i] = [starti, endi]` and `secondList[j] = [startj, endj]`. Each list of intervals is pairwise **disjoint** and in **sorted order**.

Return _the intersection of these two interval lists_.

A **closed interval** `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`.

The **intersection** of two closed intervals is a set of real numbers that are either empty or represented as a closed interval. For example, the intersection of `[1, 3]` and `[2, 4]` is `[2, 3]`.

## solution

The only difficult part of this problem is realizing what disjointness tells us about our approach. Essentially, we should start at the beginning of both arrays, and then check for overlap.

If there is overlap, we add it to our output. Then, we greedily advance the interval that _ends earlier_, and not the one that started earlier. This is because:

1. If the two intervals did overlap, then no other intervals in the other array will overlap again because it is disjoint and ascending.
2. If the two intervals didn’t overlap, then also, no other intervals will overlap because it is disjoint and ascending.

```python
def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
	n1, n2 = len(firstList), len(secondList)
	  
	if n1 == 0 or n2 == 0:
		return []
	  
	res = []
	p1 = p2 = 0
	while p1 < n1 and p2 < n2:
		lb = max(firstList[p1][0], secondList[p2][0])
		rb = min(firstList[p1][1], secondList[p2][1])
	  
		if lb <= rb:
			res.append([lb, rb])
		if firstList[p1][1] < secondList[p2][1]:
			p1 += 1
		else:
			p2 += 1
	return res
```
