---
type: leetcode
title: 480. sliding window median
tags:
  - heap
  - sorting
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-12
updated: 2024-09-12
---

The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle values.

- For examples, if `arr = [2,3,4]`, the median is `3`.
- For examples, if `arr = [1,2,3,4]`, the median is `(2 + 3) / 2 = 2.5`.

You are given an integer array `nums` and an integer `k`. There is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the median array for each window in the original array_. Answers within `10-5` of the actual value will be accepted.

## solutions

First of all, the brute force solution is to just sort each window of length `k` and grab the middle value(s). This is $O(nk\log k)$.

As a minor improvement, we can maintain a sorted list of length $k$, and remove/insert values as they exit and enter the window. Each of these operations will take $O(k)$ time, leading to a runtime of $O(nk)$.

### sorted list

This achieves $O(n\log k)$ as every operation in sorted lists is logarithmic, but it probably wouldn’t be sufficient in an interview.

```python
from sortedcontainers import SortedList
def medianSlidingWindow(self, nums: List[int], k: int) -> List[float]:
	window = SortedList()
	res = []
	  
	for i in range(len(nums)):
		window.add(nums[i])
		if i >= k:
			window.remove(nums[i-k])
		if len(window) == k:
			if k & 1:
				res.append(window[k // 2])
			else:
				res.append((window[k//2] + window[k //2-1])/2)
	return res
```

### two heaps w/ lazy deletion

This is very similar and inspired by [[295-find-median-from-data-stream]]. However, we have to figure out how we efficiently remove a value from the heaps as values fall out the left of our sliding window.

```python
def medianSlidingWindow(self, nums: List[int], k: int) -> List[float]:
	min_heap, max_heap = [], []
	removes = defaultdict(int)
	res = []
	  
	def find_median():
		if k & 1:
			return -max_heap[0]
		return (-max_heap[0]+min_heap[0]) / 2

	# this is kinda fancy but you could probably just push
	# k elements into the left half and then pop-push k//2
	# into the right half
	  
	# push first k elements into two heaps
	# either left == right or left is one bigger than right
	for i in range(k):
		# push everything onto left half first
		heappush(max_heap, -nums[i])
		# THEN, we pop to right half to maintain
		# every value in left half <= value in right
		# half without having to do any number comparison
		heappush(min_heap, -heappop(max_heap))
	  
		# this ensures that balance, bias towards left half
		# being bigger
		if len(min_heap) > len(max_heap):
			heappush(max_heap, -heappop(min_heap))
	  
	median = find_median()
	res.append(median)
	  
	# at this stage, consider the heaps balanced
	# if k is even, the heaps are same length
	# if k is odd, left half is one bigger
	  
	for i in range(k, len(nums)):
		to_remove = nums[i-k]
		removes[to_remove] += 1
	  
		# left half less values makes balance negative
		balance = -1 if to_remove <= median else 1
	  
		# push to left half
		if nums[i] <= median:
			balance += 1
			heappush(max_heap, -nums[i])
		# we know for certain that if a number is
		# bigger than the median, then it is in the
		# right half.
		else:
			balance -= 1
			heappush(min_heap, nums[i])

	# balancing step
	
	# left half too short
	if balance < 0:
		heappush(max_heap, -heappop(min_heap))
	elif balance > 0:
		heappush(min_heap, -heappop(max_heap))

	# lazy deletion step
	  
	while max_heap and removes[-max_heap[0]] > 0:
		removes[-max_heap[0]] -= 1
		heappop(max_heap)
	while min_heap and removes[min_heap[0]] > 0:
		removes[min_heap[0]] -= 1
		heappop(min_heap)
	  
	median = find_median()
	res.append(median)
	  
	return res
```
