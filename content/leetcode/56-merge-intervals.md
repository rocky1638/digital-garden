---
type: leetcode
title: 56. merge intervals
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/merge-intervals/
date: 2022-11-21
updated: 2024-08-28
tags:
  - sorting
  - array
  - intervals
---

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

## solution

First, we sort the intervals by starting time. Push new intervals into `merged` array.

If the next interval overlaps, update the top element of `merged`.

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        # sort by starting time
        intervals.sort(key=lambda x: x[0])
        
        merged = [intervals[0]]
        
        for interval in intervals[1:]:
            # if interval overlaps with most recent in merged
            if merged[-1][1] >= interval[0]:
                merged[-1][1] = max(merged[-1][1], interval[1])
            else:
                merged.append(interval)
        return merged
```
