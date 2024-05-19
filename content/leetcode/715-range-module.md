---
type: leetcode
title: 715. range module
tags:
  - intervals
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-18
---

A Range Module is a module that tracks ranges of numbers. Design a data structure to track the ranges represented as **half-open intervals** and query about them.

A **half-open interval** `[left, right)` denotes all the real numbers `x` where `left <= x < right`.

Implement the `RangeModule` class:

- `RangeModule()` Initializes the object of the data structure.
- `void addRange(int left, int right)` Adds the **half-open interval** `[left, right)`, tracking every real number in that interval. Adding an interval that partially overlaps with currently tracked numbers should add any numbers in the interval `[left, right)` that are not already tracked.
- `boolean queryRange(int left, int right)` Returns `true` if every real number in the interval `[left, right)` is currently being tracked, and `false` otherwise.
- `void removeRange(int left, int right)` Stops tracking every real number currently being tracked in the **half-open interval** `[left, right)`.

## solution

This is a lot to explain so please just watch the video linked below for in-depth details. TLDR, we maintain a disjoint list of intervals that represent the ranges we’re currently storing.

`addRange` is essentially the same problem as [[56-merge-intervals]], while `removeRange` can be solved with similar intuition (we just have to think about all the different cases between an interval, and another interval that is doing the erasing).

Finally, `queryRange` requires some clever thinking. We know that since our list of intervals is disjoint, a range query must be solved by a single interval in our list! As such, we find the interval that must be used to solve the query - we look for the interval with the highest left bound that still contains the start of our query range (we do this using `bisect_right`.) Then, if that interval’s right bound contains our query’s right bound, we have a successful search!

```python
class RangeModule:

	def __init__(self):
		self.ranges = []
  
	def addRange(self, left: int, right: int) -> None:
		new_interval = [left, right]
		  
		# insert the new interval in sorted order
		insert_idx = insort(self.ranges, new_interval)
		  
		new_ranges = []
		  
		# merge any overlapping intervals for disjointness
		for interval in self.ranges:
			# all the intervals before new one
			if interval[1] < new_interval[0]:
				new_ranges.append(interval)
		  
			# no overlap with previous interval
			if len(new_ranges) == 0 or interval[0] > new_ranges[-1][1]:
				new_ranges.append(interval)
		  
			# overlap
			if interval[0] <= new_ranges[-1][1]:
				new_ranges[-1] = [
					min(interval[0], new_ranges[-1][0]),
					max(interval[1], new_ranges[-1][1])
				]
		  
		self.ranges = new_ranges
  
	def queryRange(self, left: int, right: int) -> bool:
		query = [left, right]
		  
		# find rightmost interval where interval[0] <= query[0]
		# NOTE: we set the right value in query to a large number to ensure
		# it always ends up to the right of any interval that shares the same
		# left bound
		best_interval_idx = bisect_right(self.ranges, [left, 1e9])
		if best_interval_idx == 0 or len(self.ranges) == 0:
			return False
		  
		best_interval = self.ranges[best_interval_idx-1]
		return best_interval[1] >= query[1]
	  
	def removeRange(self, left: int, right: int) -> None:
		# iterate through disjoint set of ranges, and
		# remove/trim any intervals that overlap
		to_remove = [left, right]
		  
		new_ranges = []
		for interval in self.ranges:
			if self._hasOverlap(interval, to_remove):
				result = self._remove(interval, to_remove)
				if result is None:
					continue
				new_ranges.extend(result)

			else:
				new_ranges.append(interval)
		  
		self.ranges = new_ranges
	
	def _hasOverlap(self, i1, i2):
		# i1 always has the smaller left bound
		if i1[0] > i2[0]:
			i1, i2 = i2, i1
		  
		return i2[0] <= i1[1]
	  
	def _remove(self, source, to_remove):
		# total overlap
		if to_remove[0] <= source[0] and to_remove[1] >= source[1]:
			return None
		# left overlap
		if to_remove[1] >= source[0] and to_remove[0] <= source[0]:
			return [[to_remove[1], source[1]]]
		  
		# inner overlap
		if source[0] < to_remove[0] and source[1] > to_remove[1]:
			return [[source[0], to_remove[0]], [to_remove[1], source[1]]]
		# right overlap
		if to_remove[0] <= source[1] and to_remove[1] >= source[1]:
			return [[source[0], to_remove[0]]]
```

## references

- https://www.youtube.com/watch?v=OLoBBLvU2KY
