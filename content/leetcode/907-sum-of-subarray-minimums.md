---
type: leetcode
title: 907. sum of subarray minimums
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-24
---

Given an array of integers arr, find the sum of `min(b)`, where `b` ranges over every (contiguous) subarray of `arr`. Since the answer may be large, return the answer **modulo** `109 + 7`.

## solution

If we figure out how far we can extend in the left and right for each number at index $i$ while maintaining that `arr[i]` is the minimum, we can then enumerate all the possible subarrays based on the number of places to place the “[” or “]” on either side.

To find these bounds, we essentially just want to find the next and previous smaller element, for each element in the array. We do this using a [[monotonic-stack]].

```python
def sumSubarrayMins(self, arr: List[int]) -> int:
	n = len(arr)
	bounds = [[-1, n] for i in range(len(arr))]
	stack = []
	  
	for i in range(n):
		while stack and arr[stack[-1]] > arr[i]:
			# i is popped's NSE
			popped_idx = stack.pop()
			bounds[popped_idx][1] = i
	  
		# stack[-1] is i's PSE
		if stack:
			bounds[i][0] = stack[-1]
		stack.append(i)
	  
	ans = 0
	for i, (lb, rb) in enumerate(bounds):
		lmult = i-lb
		rmult = rb-i
		ans += lmult * rmult * arr[i]
	  
	return ans % (10**9+7)
```
