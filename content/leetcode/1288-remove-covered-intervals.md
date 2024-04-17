---
type: leetcode
title: "1288. remove covered intervals"
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-04-17
---

Given an array `intervals` where `intervals[i] = [li, ri]` represent the interval `[li, ri)`, remove all intervals that are covered by another interval in the list.

The interval `[a, b)` is covered by the interval `[c, d)` if and only if `c <= a` and `b <= d`.

Return _the number of remaining intervals_.

## solution

Some intuition:

1. Given two intervals $[a,b]$ and $[c,d]$, if $a \lt c$, then it is impossible for $[a,b]$ to be covered by $[c,d]$.
2. If $[a,b]$ does cover $[c,d]$, such that $b \ge d$, then $[a,b]$ could continue to cover the next interval, when sorted by starting point (let’s call it $[e,f]$).
3. If $[a,b]$ does not cover $[c,d]$ (this means that $d \ge b$), then we know that if $[e,f]$ were to be covered by $[a,b]$, it will also be covered by $[c,d]$.

Given this intuition, we first sort the intervals by starting time, and then by descending ending time (this is for the edge case illustrated by the test case `[[1,2], [1,4]]`).

Then, we check if two intervals are in a covering relationship. If they are, we mark the interval as covered by decrementing `ans`, and then incrementing the covered pointer `cur`, because the covering interval at `prev` could continue to cover more intervals.

Else, we update `prev` to be equal to the `cur` counter, and increment `cur`, because of the intuition described in (3) above.

```python
def removeCoveredIntervals(self, intervals: List[List[int]]) -> int:
	intervals.sort(key=lambda x: (x[0],-x[1]))
	prev, cur = 0, 1
	ans = len(intervals)
	  
	while cur < len(intervals):
		# prev covers cur
		if intervals[prev][0] <= intervals[cur][0] and intervals[prev][1] >= intervals[cur][1]:
			ans -= 1
			# prev could cover more, so keep prev pointer there
			cur += 1
		else:
			# prev doesn't cover cur, so
			# update prev to cur, and increment cur
			prev = cur
			cur += 1
	return ans
```
