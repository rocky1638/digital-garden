---
title: 1851. minimum interval to include each query
type: leetcode
aliases: 
difficulty: 🔴
link: https://leetcode.com/problems/minimum-interval-to-include-each-query/
date: 2023-01-16
updated: 2024-05-17
tags:
  - heap
  - sorting
  - intervals
---

You are given a 2D integer array `intervals`, where `intervals[i] = [lefti, righti]` describes the `ith` interval starting at `lefti` and ending at `righti` **(inclusive)**. The **size** of an interval is defined as the number of integers it contains, or more formally `righti - lefti + 1`.

You are also given an integer array `queries`. The answer to the `jth` query is the **size of the smallest interval** `i` such that `lefti <= queries[j] <= righti`. If no such interval exists, the answer is `-1`.

Return _an array containing the answers to the queries_.

## solution

### brute force

We can brute force the solution by running each query $q$ across each interval $i$, for a runtime of $O(mn)$. This times out.

### priority queue

An intuition is that if we sort the intervals and queries, then we can “stop early” once an interval’s end is smaller than the query we’re currently looking at.

Also, if an interval starts after our query, we don’t have to consider it yet. For this ongoing sorted behavior, we use a heap.

So, we iterate through intervals by starting time, and the queries ascending as well. For each query, we push all potential solution intervals into the heap, which is a min-heap sorted first by smallest interval length, and then smallest ending value.

We then pop values off of the heap until we reach a valid one. We need to do this because it’s possible that the value at the head of the heap is no longer valid (i.e. the end of the interval is behind our current query).

After lazily deleting the values at the head of the heap, we are guaranteed to have the answer to our query $q$ at the top of the heap.

```python
def minInterval(self, intervals: List[List[int]], queries: List[int]):
	# sort intervals by start-time, descending
	intervals = sorted(intervals, key=lambda x: -x[0])
	
	pq = []
	res = {}
	
	for q in sorted(queries):
		# start time encompasses q
		while intervals and intervals[-1][0] <= q:
			start, end = intervals.pop()
			# interval encompasses q
			if end >= q:
				heappush(pq, (end-start+1, end))
	
		# pop all intervals that now end before q
		while pq and pq[0][1] < q:
			heappop(pq)
	
		res[q] = pq[0][0] if pq else -1
	
	return [res[q] for q in queries]
```

## references

<iframe width="560" height="315" src="https://www.youtube.com/embed/5hQ5WWW5awQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### neetcode notes

- [00:05](https://www.youtube.com/watch?v=5hQ5WWW5awQ#t=5.882038881744385) problem walkthrough and description.
- [03:03](https://www.youtube.com/watch?v=5hQ5WWW5awQ#t=183.3793439408722) brute force solution.
	- for every query, just scan every interval.
	- $O(mn)$.
- [05:00](https://www.youtube.com/watch?v=5hQ5WWW5awQ#t=300.96186803433227) walkthrough of optimal solution.
	- we sort the intervals and the queries.
	- go through the intervals until the start value is past the query, when we can stop early.
	- we keep a min heap of lengths of the intervals that satisfy a query, as well as the end position of each of these intervals.
		- we keep track of the end of the interval to make sure to lazy delete these intervals from the heap if our query starts after the end time of the interval.
