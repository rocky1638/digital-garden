---
type: leetcode
title: 1856. maximum subarray min-product
tags:
  - monotonic-stack
  - prefix-sums
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-24
---

The **min-product** of an array is equal to the **minimum value** in the array **multiplied by** the array's **sum**.

- For example, the array `[3,2,5]` (minimum value is `2`) has a min-product of `2 * (3+2+5) = 2 * 10 = 20`.

Given an array of integers `nums`, return _the **maximum min-product** of any **non-empty subarray** of_ `nums`. Since the answer may be large, return it **modulo** `109 + 7`.

Note that the min-product should be maximized **before** performing the modulo operation. Testcases are generated such that the maximum min-product **without** modulo will fit in a **64-bit signed integer**.

A **subarray** is a **contiguous** part of an array.

## solutions

The main intuition here is that to solve by hand, we probably pick a value to be our subarray minimum, and then expand outwards to see how big we can make that subarray.

To do this in code, we need to know the bounds of each of these subarrays. To do this, we need to find previous and next smaller elements, which can be done efficiently with a monotonic stack.

Then, just use prefix sums to efficiently calculate the scores.

I present two ways to do the monotonic stack part below.

### monotonic stack + prefix sums

> [!info]
> For the test case `[2,2,2,2,2]`, this code returns `prev_smaller = [-1,-1,-1,-1,-1]` and `next_smaller=[5,5,5,5,5]`.

```python
def maxSumMinProduct(self, nums: List[int]) -> int:
	n = len(nums)
	next_smaller = [n]*n
	prev_smaller = [-1]*n
	prefix_sums = [0]
	  
	stack = []
	for i, num in enumerate(nums):
		prefix_sums.append(prefix_sums[-1] + num)
		while stack and nums[stack[-1]] > num:
			next_smaller[stack[-1]] = i
			stack.pop()
		stack.append(i)
	  
	stack = []
	for i, num in reversed(list(enumerate(nums))):
		while stack and nums[stack[-1]] > num:
			prev_smaller[stack[-1]] = i
			stack.pop()
		stack.append(i)

	ans = 0
	for i in range(n):
		lb, rb = prev_smaller[i], next_smaller[i]
		su = prefix_sums[rb] - prefix_sums[lb+1]
		ans = max(ans, su*nums[i])
	return ans % (10**9+7)
```

### one-pass monotonic stack

We can use a single pass to find previous and next smaller elements, although it’s a little bit scuffed.

Essentially, my `next_smaller` finds the next strictly smaller element, continuing rightward on values that are equal.

However, `prev_smaller` stops when it sees an equal value.

For the context of this problem, it ends up working, because in cases where there are duplicates in the array, the leftmost instance of that value will expand fully rightward, getting the best answer. However, it is a little bit scuffed - we would ideally want all of the duplicate values looking as far left and right as they should be.

> [!info]
> For the test case `[2,2,2,2,2]`, this code returns `prev_smaller = [-1,0,1,2,3]` and `next_smaller=[5,5,5,5,5]`.

We can do this better with a two-pass approach.

```python
def maxSumMinProduct(self, nums: List[int]) -> int:
	n = len(nums)
	next_smaller = [n]*n
	prev_smaller = [-1]*n
	prefix_sums = [0]
	  
	stack = []
	for i, num in enumerate(nums):
		prefix_sums.append(prefix_sums[-1] + num)

		# maintain monotonicity
		while stack and nums[stack[-1]] > num:
			# record next smaller
			next_smaller[stack[-1]] = i
			stack.pop()
	  
		# if stack is non-empty, then i's
		# prev smaller is stack[-1]
		if stack:
	prev_smaller[i] = stack[-1]
	  
	# add i to stack
	stack.append(i)
	  
	ans = 0
	for i in range(n):
	lb, rb = prev_smaller[i], next_smaller[i]
	su = prefix_sums[rb] - prefix_sums[lb+1]
	ans = max(ans, su*nums[i])
	return ans % (10**9+7)
```
