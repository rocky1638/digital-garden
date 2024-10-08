---
type: leetcode
title: 857. minimum cost to hire k workers
tags:
  - heap
  - sorting
  - greedy
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-22
updated: 2024-09-22
---

There are `n` workers. You are given two integer arrays `quality` and `wage` where `quality[i]` is the quality of the `ith` worker and `wage[i]` is the minimum wage expectation for the `ith` worker.

We want to hire exactly `k` workers to form a **paid group**. To hire a group of `k` workers, we must pay them according to the following rules:

1. Every worker in the paid group must be paid at least their minimum wage expectation.
2. In the group, each worker's pay must be directly proportional to their quality. This means if a worker’s quality is double that of another worker in the group, then they must be paid twice as much as the other worker.

Given the integer `k`, return _the least amount of money needed to form a paid group satisfying the above conditions_. Answers within `10-5` of the actual answer will be accepted.

## solution

```python
def mincostToHireWorkers(self, quality: List[int], wage: List[int], k: int) -> float:
	"""
	brute force:
	- enumerate every possible k selection O(nk)
	  
	wage = [50, 30, 70]
	quality = [20, 5, 10]
	sorted(wage_ratio) = [2.5, 6, 7]
	  
	optimizations:
	- sort by wage ratio ("unit cost")
	- for a group of k workers, all workers will need
	to be paid at the rate of the highest unit cost worker out of them
	- so, first try to take the k cheapest/unit workers
	- then, sliding window, take the next cheapest/unit worker -- this will be
	the new unit cost for every worker
	- we have to evict someone... since they all use this new worker's unit
	cost, just lay off the highest quality worker (use a heap)
	"""
	  
	combined = [(quality, wage, wage/quality) for quality, wage in zip(quality, wage)]
	combined.sort(key=lambda x: x[2])
	  
	# choose first k workers
	max_heap = []
	unit_cost = 0
	total_qual = 0

	for i in range(k):
		q, w, r = combined[i]
		total_qual += q
		heappush(max_heap, -q)
		unit_cost = r

	res = total_qual * unit_cost
	for i, (q, w, r) in enumerate(combined[k:]):
		# pop worker
		popped_q = -heappop(max_heap)
		total_qual -= popped_q
	  
		# set new unit cost
		# (because we're sorted by unit_cost ASC)
		unit_cost = r
		total_qual += q
		heappush(max_heap, -q)
	  
		res = min(res, total_qual * unit_cost)
	  
	return res
```
