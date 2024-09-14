---
created_at: 2023-01-16
type: leetcode
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/non-overlapping-intervals/
---

# 435. Non-overlapping Intervals

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return _the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping_.

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        """
        - if we sort the array by start time,
          then when we find two intervals that overlap,
          we always go with the one that has an earlier end time (greedy).
        """
        intervals.sort(key=lambda x: x[0])

        acc = [intervals[0]]
        for start, end in intervals[1:]:
            prev = acc[-1]
            if prev[1] > start: # if overlap
                # keep the interval that ends earlier
                if end > prev[1]:
                    continue
                else:
                    acc.pop()
                    acc.append([start, end])
            # no overlap
            else:
                acc.append([start, end])
        
        return len(intervals) - len(acc)
```

- we use standard interval concepts, but it is also greedy.
- we first sort the intervals by start time, and then go through them, appending them to an array that contains no overlaps.
	- if we find two adjacent ones that overlap, always favor the one that ends earlier becaues it is strictly better in terms of a lower chance of clashing with the future ones that we will append.

```dataview
table without id file.inlinks as Backlinks
where file.name = this.file.name
```

## Related.

## References.

Categories:: [[intervals]], [[greedy]], [[sorting]], [[array]]
