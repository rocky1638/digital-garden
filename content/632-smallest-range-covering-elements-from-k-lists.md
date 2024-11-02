---
type: leetcode
title: 632. smallest range covering elements from k lists
tags:
  - heap
  - sliding-window
  - hashmap
aliases: 
parents:
  - "[[23-merge-k-sorted-lists]]"
children: 
supports: 
enemies: 
date: 2024-10-29
updated: 2024-10-29
---

You have `k` lists of sorted integers in **non-decreasing order**. Find the **smallest** range that includes at least one number from each of the `k` lists.

We define the range `[a, b]` is smaller than range `[c, d]` if `b - a < d - c` **or** `a < c` if `b - a == d - c`.

## solution

### merge k lists + sliding window

```python
def smallestRange(self, nums: List[List[int]]) -> List[int]:
	def merge():
	merged = []
	minheap = [(nums[k][0], k, 0) for k in range(len(nums))]
	heapify(minheap)
	  
	while minheap:
		val, list_id, list_idx = heappop(minheap)
		merged.append((val, list_id))
		if list_idx+1 < len(nums[list_id]):
			heappush(
				minheap,
				(nums[list_id][list_idx+1], list_id, list_idx+1)
			)
		return merged

	merged = merge()
	  
	# sliding window
	best = inf
	res = []
	# counts per list_id
	counts = defaultdict(int)
	# list id's currently in window
	seen = set()
	l = 0
	for r in range(len(merged)):
		val, list_id = merged[r]

		# add merged[r] to window
		counts[list_id] += 1
		if counts[list_id] == 1:
			seen.add(list_id)

		# slide window up left until invalid
		while len(seen) == len(nums):
			if merged[r][0]-merged[l][0] < best:
				res = [merged[l][0], merged[r][0]]
				best = merged[r][0]-merged[l][0]

			_, remove_list_id = merged[l]
			counts[remove_list_id] -= 1
			if counts[remove_list_id] == 0:
				seen.remove(remove_list_id)
			l += 1

	return res
```
