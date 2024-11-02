---
type: leetcode
title: 275. h-index ii
tags:
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-14
updated: 2024-10-14
---

Given an array of integers `citations` where `citations[i]` is the number of citations a researcher received for their `ith` paper and `citations` is sorted in **ascending order**, return _the researcher's h-index_.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): The h-index is defined as the maximum value of `h` such that the given researcher has published at least `h` papers that have each been cited at least `h` times.

You must write an algorithm that runs in logarithmic time.

## solution

```python
def hIndex(self, citations: List[int]) -> int:
	n = len(citations)
	l, r = 0, n - 1
	  
	def valid(m):
		# n-m is number of values in array >= citations[m]
		# we need at least n-m values >= citations[m] for h-index
		# of (n-m) to be valid
		return citations[m] >= n-m
	  
	while l <= r:
		m = (l + r) // 2
		if valid(m) and (m == 0 or not valid(m-1)):
			return n-m
		# Check if the current m is a valid h-index candidate
		elif valid(m):
			# If valid, move left to see if we can find a higher h-index
			r = m - 1
		else:
			# If not valid, move right
			l = m + 1

	# if we exit loop without returning,
	# then there was no valid index
	return 0
```
