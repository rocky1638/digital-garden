---
type: leetcode
title: 57. insert interval
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/insert-interval/
date: 2022-11-15
updated: 2024-09-11
---

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` _after the insertion_.

**Note** that you don't need to modify `intervals` in-place. You can make a new array and return it.

## solution

- make another array `ans`, and first append all the intervals that come strictly before the `newInterval`.
- then for the rest of the intervals including `newInterval`, we will merge with the interval at the end of the array `ans` if they overlap.

```python
def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
	ans = []
	  
	def merge_add(interval):
		x1, x2 = interval
		if not ans or x1 > ans[-1][1]: # no overlap
			ans.append([x1, x2])
		else:
			ans[-1] = [min(x1, ans[-1][0]), max(x2, ans[-1][1])]
	  
	i = 0
	# add all intervals that start before newInterval
	while i < len(intervals):
		if intervals[i][0] < newInterval[0]:
			ans.append(intervals[i])
			i += 1
		else:
			break
	  
	# add and merge if necessary new interval
	merge_add(newInterval)
	
	# add remaining intervals, merging each if necessary
	while i < len(intervals):
		merge_add(intervals[i])
		i += 1

	return ans
```
