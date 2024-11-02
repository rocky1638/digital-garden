---
type: leetcode
title: 2406. divide intervals into minimum number of groups
tags:
  - heap
  - line-sweep
  - sorting
aliases: 
parents:
  - "[[253-meetings-rooms-ii]]"
children: 
supports: 
enemies: 
date: 2024-10-22
updated: 2024-10-22
---

You are given a 2D integer array `intervals` where `intervals[i] = [lefti, righti]` represents the **inclusive** interval `[lefti, righti]`.

You have to divide the intervals into one or more **groups** such that each interval is in **exactly** one group, and no two intervals that are in the same group **intersect** each other.

Return _the **minimum** number of groups you need to make_.

Two intervals **intersect** if there is at least one common number between them. For example, the intervals `[1, 5]` and `[5, 8]` intersect.

## solutions

This problem is the exact same as [[253-meetings-rooms-ii]].

### sorting + heap

```python
# O(nlogn + nlogk), where k is answer
def minGroups(self, intervals: List[List[int]]) -> int:
	res = 0
	# min-heap of end times
	active_meetings = []
	  
	intervals.sort(key=lambda x: x[0])
	for start, end in intervals:
		while active_meetings and active_meetings[0] < start:
			heappop(active_meetings)
		heappush(active_meetings, end)
	  
		res = max(res, len(active_meetings))

	return res
```

### line-sweep

```python
# O(nlogn)
def minGroups(self, intervals: List[List[int]]) -> int:
	START, END = 0, 1
	  
	events = []
	for start, end in intervals:
		events.append((start, START))
		events.append((end, END))
	events.sort(key=lambda x: (x[0], x[1]))
	  
	res = 0
	active_groups = 0
	for event in events:
		if event[1] == START:
			active_groups += 1
			res = max(res, active_groups)
		else:
			active_groups -= 1
	return res
```
