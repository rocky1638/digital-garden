---
type: leetcode
title: 31. next permutation
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/next-permutation/
date: 2022-12-09
updated: 2024-08-29
tags:
  - two-pointer
  - array
---

A **permutation** of an array of integers is an arrangement of its members into a sequence or linear order.

- For example, for `arr = [1,2,3]`, the following are all the permutations of `arr`: `[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]`.

The **next permutation** of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the **next permutation** of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

- For example, the next permutation of `arr = [1,2,3]` is `[1,3,2]`.
- Similarly, the next permutation of `arr = [2,3,1]` is `[3,1,2]`.
- While the next permutation of `arr = [3,2,1]` is `[1,2,3]` because `[3,2,1]` does not have a lexicographical larger rearrangement.

Given an array of integers `nums`, _find the next permutation of_ `nums`.

The replacement must be **[in place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

## solution

You just have to figure out the pattern of how to find the next largest permutation number, thinking about how numbers are valued (least significant bits).

```python
def nextPermutation(self, nums: List[int]) -> None:
	"""
	find next largest elem in decreasing portion that is larger than
	the value to the left of the decreasing suffix
	swap them, and then reverse the decreasing to increasing
	"""
	def reverse(l, r):
		while l < r:
			nums[l], nums[r] = nums[r], nums[l]
			l += 1
			r -= 1
	  
	n = len(nums)
	r = n-1
	  
	# 1. find decreasing suffix
	while r >= 1 and nums[r-1] >= nums[r]:
		r -= 1

	# if all decreasing, return all increasing
	if r == 0:
		reverse(0, n-1)
		return
	  
	# r is on first element of descending suffix
	suffix_start = r
	swap_idx = suffix_start-1
	  
	# set r to next largest value larger than nums[swap_idx]
	r = n-1
	while nums[r] <= nums[swap_idx]:
		r -= 1
	  
	# swap values, and reverse suffix
	nums[r], nums[swap_idx] = nums[swap_idx], nums[r]
	reverse(suffix_start, n-1)
```
