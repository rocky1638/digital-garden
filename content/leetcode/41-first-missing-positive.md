---
type: leetcode
title: 41. first missing positive
tags:
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-06
updated: 2024-10-06
---

Given an unsorted integer array `nums`. Return the _smallest positive integer_ that is _not present_ in `nums`.

You must implement an algorithm that runs in `O(n)` time and uses `O(1)` auxiliary space.

## solution

The easy brute force way to do this could be to put all of the array values in a set, and then just iterate up from 1 until we find a value that doesn’t exist in the set.

However, to do it in constant space, we need to make use of the input array. Getting to this solution requires some intuition.

1. Of the $n$ values in our array `nums`, we either have all the values from 1 to $n$ in the array, or we don’t.
	- If we have all of the values, then our first missing positive is just $n+1$.
	- If we don’t, then our first missing positive _must_ lie in the range $[1,n]$.

Due to this realization, we realize that we only need to check if the values in the range $[1,n]$ exist in our array. We can track this in constant space by flipping values in our input array based on their index (e.g. if 1 is found in the array, make the value at `nums[0]` negative).

Before we do this, we should remove any values that are bigger than $n$ or $\le 0$.

```python
def firstMissingPositive(self, nums: List[int]) -> int:
	n = len(nums)
	for i, num in enumerate(nums):
		if num <= 0 or num > n:
			nums[i] = n+1

	for i in range(n):
		if abs(nums[i]) <= n:
			# handle duplicate numbers
			if nums[abs(nums[i])-1] < 0:
				continue
			nums[abs(nums[i])-1] *= -1

	for i in range(1, n+1):
		if nums[i-1] > 0:
			return i
	return n+1
```
