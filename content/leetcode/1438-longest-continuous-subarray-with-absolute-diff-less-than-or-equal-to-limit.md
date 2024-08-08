---
type: leetcode
title: 1438. longest continuous subarray with absolute diff less than or equal to limit
tags:
  - sliding-window
  - heap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-06
---

Given an array of integers `nums` and an integer `limit`, return the size of the longest **non-empty** subarray such that the absolute difference between any two elements of this subarray is less than or equal to `limit`_._

## solution

The question is pretty obviously a sliding window problem, but the hard part is how to keep track of validity as we’re sliding.

We notice that we only care about the minimum and maximum values at any point in time, and to do that efficiently, we can use two heaps. The key here is to lazily delete from the heaps as we shorten our window from the left, very similar to the strategy used in [[239-sliding-window-maximum]].

```python
def longestSubarray(self, nums: List[int], limit: int) -> int:
	# these might contain lazily deleted values
	min_heap = []
	max_heap = []
	ans = 0
	  
	def pruneHeaps(idx):
		while min_heap and min_heap[0][1] < l:
			heappop(min_heap)
		while max_heap and max_heap[0][1] < l:
			heappop(max_heap)
	  
	l = 0
	for r in range(len(nums)):
		num = nums[r]
	  
		# add new value to subarray
		heappush(min_heap, (num, r))
		heappush(max_heap, (-num, r))
		  
		# shrink window until valid
		while l < r:
			diff = abs(min_heap[0][0] + max_heap[0][0])

			if diff <= limit:
				break
		  
			l += 1
			# make sure heap is valid
			# going into next iteration
			pruneHeaps(l)
		ans = max(ans, r-l+1)
	return ans
```
