---
type: leetcode
title: 493. reverse pairs
tags:
  - merge-sort
  - two-pointer
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-21
updated: 2024-09-21
---

Given an integer array `nums`, return _the number of **reverse pairs** in the array_.

A **reverse pair** is a pair `(i, j)` where:

- `0 <= i < j < nums.length` and
- `nums[i] > 2 * nums[j]`.

## solutions

### brute force

Obvious.

```python
def reversePairs(self, nums: List[int]) -> int:
	n = len(nums)
	res = 0
	for i in range(n):
		for j in range(i+1, n):
			if nums[i] > nums[j] * 2:
				res += 1
	return res
```

### modified merge sort

The main intuition required here is:

> If we had two sorted arrays, we could figure out how many reverse pairs exist where `i` is in the first array and `j` is in the second array in linear time (using two pointers).

The logical next step is that we can run a merge sort, and calculate the number of reverse pairs between two subarrays as we’re merging it.

```python
def reversePairs(self, nums: List[int]) -> int:
	n = len(nums)
	res = 0
	  
	def merge(arr1, arr2):
		nonlocal res

		# first, figure out how many reverse pairs
		p1 = p2 = 0
		while p1 < len(arr1) and p2 < len(arr2):
			if arr1[p1] > arr2[p2] * 2:
				res += len(arr1)-p1
				p2 += 1
			else:
				p1 += 1
	  
		# merge
		out = []
		p1 = p2 = 0
		while p1 < len(arr1) and p2 < len(arr2):
			if arr1[p1] < arr2[p2]:
				out.append(arr1[p1])
				p1 += 1
			else:
				out.append(arr2[p2])
				p2 += 1
		while p1 < len(arr1):
			out.append(arr1[p1])
			p1 +=1
		while p2 < len(arr2):
			out.append(arr2[p2])
			p2 += 1
		return out
	  
	def mergesort(nums):
		nonlocal res
		if len(nums) <= 1:
			return nums

		m = len(nums) // 2
		lsorted = mergesort(nums[:m])
		rsorted = mergesort(nums[m:])
		return merge(lsorted, rsorted)

	mergesort(nums)
	return res
```

### segment tree

TODO

```python
```
