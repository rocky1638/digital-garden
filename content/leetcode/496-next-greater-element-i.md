---
type: leetcode
title: 496. next greater element i
tags:
  - monotonic-stack
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-20
---

The **next greater element** of some element `x` in an array is the **first greater** element that is **to the right** of `x` in the same array.

You are given two **distinct 0-indexed** integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the **next greater element** of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

Return _an array_ `ans` _of length_ `nums1.length` _such that_ `ans[i]` _is the **next greater element** as described above._

## solution

```python
def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
	d = {}
	stack = []
	  
	for num in nums2:
		while stack and stack[-1] < num:
			popped = stack.pop()
			d[popped] = num
		stack.append(num)

	while stack:
		d[stack.pop()] = -1

	return [d[n] for n in nums1]
```

## references

- [https://youtu.be/Du881K7Jtk8](https://youtu.be/Du881K7Jtk8 "Share link")
