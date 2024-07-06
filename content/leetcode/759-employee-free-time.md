---
type: leetcode
title: 759. employee free time
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-27
---

We are given a list `schedule` of employees, which represents the working time for each employee.

Each employee has a list of non-overlapping `Intervals`, and these intervals are in sorted order.

Return the list of finite intervals representing **common, positive-length free time** for _all_ employees, also in sorted order.

(Even though we are representing `Intervals` in the form `[x, y]`, the objects inside are `Intervals`, not lists or arrays. For example, `schedule[0][0].start = 1`, `schedule[0][0].end = 2`, and `schedule[0][0][0]` is not defined).  Also, we wouldn't include intervals like [5, 5] in our answer, as they have zero length.

## solution

Pretty simple interval question, despite it being a hard. We keep a min-heap with the next interval for each employee. The idea here is just to merge all of the employees’ free times in a disjoint list of sorted intervals, and then just find the gaps in-between.

```python
def employeeFreeTime(self, schedule: '[[Interval]]') -> '[Interval]':
	n = len(schedule)
	h = [(employee[0].start, employee[0].end, i, 0) for i, employee in enumerate(schedule)]
	heapq.heapify(h)
	  
	# disjoint invariant
	merged = []
	while h:
		s, e, i, ptr = heappop(h)
		new_interval = [s, e]
		while merged and merged[-1][1] > s:
			to_merge = merged.pop()
			new_interval = [min(s, to_merge[0]), max(e, to_merge[1])]

		merged.append(new_interval)
		if ptr+1 < len(schedule[i]):
			heappush(h, (
				schedule[i][ptr+1].start,
				schedule[i][ptr+1].end, i, ptr+1)
			)
	  
	ans = []
	for (s1, e1), (s2, e2) in zip(merged[:-1], merged[1:]):
		if e1 < s2:
			ans.append(Interval(e1, s2))
	return ans
```
