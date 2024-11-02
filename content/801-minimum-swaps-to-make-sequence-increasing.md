---
type: leetcode
title: 801. minimum swaps to make sequence increasing
tags:
  - recursion
  - memoization
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-25
updated: 2024-10-25
---

You are given two integer arrays of the same length `nums1` and `nums2`. In one operation, you are allowed to swap `nums1[i]` with `nums2[i]`.

- For example, if `nums1 = [1,2,3,8]`, and `nums2 = [5,6,7,4]`, you can swap the element at `i = 3` to obtain `nums1 = [1,2,3,4]` and `nums2 = [5,6,7,8]`.

Return _the minimum number of needed operations to make_ `nums1` _and_ `nums2` _**strictly increasing**_. The test cases are generated so that the given input always makes it possible.

An array `arr` is **strictly increasing** if and only if `arr[0] < arr[1] < arr[2] < ... < arr[arr.length - 1]`.

## solution

To enumerate possible solutions, we need to know if the previous value was swapped, because we only ever have to lookback by 1 value.

```python
# O(2n)
def minSwap(self, nums1: List[int], nums2: List[int]) -> int:
	memo = {}
	  
	def recurse(idx, prev_swapped):
		if idx == len(nums1):
			return 0
		if (idx, prev_swapped) in memo:
			return memo[(idx, prev_swapped)]
	  
		p1 = nums1[idx-1] if idx > 0 else -1
		p2 = nums2[idx-1] if idx > 0 else -1
		  
		if prev_swapped:
			p1, p2 = p2, p1
		ans = inf
	  
		# NOTE: we try BOTH of these if they are both valid,
		# because we could swap at an index even if it's not
		# strictly required:
		# consider nums1=[0,4,4,5,9], nums2=[0,1,6,8,10]
		  
		# Option 1: No swap at idx (if it maintains order)
		if nums1[idx] > p1 and nums2[idx] > p2:
			ans = min(ans, recurse(idx + 1, False))

		# Option 2: Swap at idx (if it maintains order after swap)
		if nums1[idx] > p2 and nums2[idx] > p1:
			ans = min(ans, 1 + recurse(idx + 1, True))
		  
		memo[(idx, prev_swapped)] = ans
		return ans

	return recurse(0, False)
```
