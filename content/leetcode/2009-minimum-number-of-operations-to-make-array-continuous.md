---
type: leetcode
title: 2009. minimum number of operations to make array continuous
tags:
  - binary-search
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-06
updated: 2024-07-06
---

You are given an integer array `nums`. In one operation, you can replace **any** element in `nums` with **any** integer.

`nums` is considered **continuous** if both of the following conditions are fulfilled:

- All elements in `nums` are **unique**.
- The difference between the **maximum** element and the **minimum** element in `nums` equals `nums.length - 1`.

For example, `nums = [4, 2, 5, 3]` is **continuous**, but `nums = [1, 2, 3, 5, 6]` is **not continuous**.

Return _the **minimum** number of operations to make_ `nums` **_continuous_**.

## solution

First of all, there is some time required to distill and simplify what a continuous array means. Essentially, it’s an array that will contain all the $n$ consecutive values from some small value $l$ to large value $r$ such that $r-l+1 = n$.

With this in mind, we realize that (ignoring duplicates for now), we just need to set window bounds of $l$ and $r$, and then determine how many of the values in the array lie outside of those values. This is the number of replace operations we’ll need to fix the array to be continuous within the range $[l, r]$.

We do this by first sorting the array, then iterating through each value in the array and setting it to $l$. Then we calculate $r$, and use binary search to find the right-bias insertion point, to determine how many values lie outside of the range.

For duplicates, an intuition is that we can first iterate through the array, and set any duplicates to some sentinel value like `inf`, so that they always sit to the right on the sorted array. Then, if we do the same process, they will always lie outside of the $[l,r]$ window, and will need replacement actions.

This is an option, but another way to do this is to simply remove them from the array but keep $n$ as the original array length. The way that I’m calculating the number of values to the right of $r$ will then behave the same way as if we just set those values to `inf`.

```python
def minOperations(self, nums: List[int]) -> int:
	n = len(nums)
	nums = sorted(set(nums))
	  
	ans = inf
	for i, num in enumerate(nums):
		right_val = num+n-1
		right_idx = bisect.bisect_right(nums, right_val)
	  
		ans = min(
			ans,
			i + (n-right_idx)
		)
	return ans
```
