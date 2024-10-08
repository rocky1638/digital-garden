---
type: leetcode
title: 713. subarray product less than k
tags:
  - binary-search
  - prefix-sums
  - sliding-window
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-22
updated: 2024-09-22
---

Given an array of integers `nums` and an integer `k`, return _the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than_ `k`.

## solutions

### linear prefix product

Instead of brute-forcing every possible subarray and checking which would be $O(n^3)$, we can maintain a prefix product array, and find the longest subarray extending to the left from some index $i$ that is $< k$.

Because all values in `nums` are positive, we know that every shorter subarray is also valid.

```python
# O(n^2)
def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
	res = 0
	prefix_products = [1]
	  
	prefix = 1
	for i in range(len(nums)):
		prefix *= nums[i]
	  
		for j in range(i+1):
			# we're ok with just a floor function here
			if prefix // prefix_products[j] < k:
				res += i-j+1
				break
		prefix_products.append(prefix)

	return res
```

### prefix products w/ binary search

We notice that prefix sums is strictly non-decreasing, so we can binary search for the leftmost valid value instead of linearly searching.

```python
# O(nlogn)
def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
	res = 0
	prefix_products = [1]

	# O(logn)
	def binary_search(i, total):
		# [1, 10, 50, 100, 600]
		l, r = 0, i
		while l <= r:
			m = (l+r)//2
			prev = prefix_products[m]
	  
			if total // prev < k and (m == 0 or total // prefix_products[m-1] >= k):
				return m
			elif total // prev >= k:
				l = m + 1
			else:
				r = m - 1
		return -1
	  
	prefix = 1
	for i in range(len(nums)):
		prefix *= nums[i]
		left_bound = binary_search(i, prefix)
		if left_bound >= 0:
			res += i-left_bound+1
		prefix_products.append(prefix)
	return res
```

### sliding window

We can use a standard sliding window approach to achieve linear runtime.

Remember that we might have to downsize our window down to an empty window (when $l > r$) because `nums[i]` could be greater than $k$.

```python
def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
	res = 0
	l = 0
	product = 1

	for r in range(len(nums)):
		# add value to window
		product *= nums[r]

		# decrease window until valid
		# (or until window is empty i.e. l = r+1)
		while l <= r and product >= k:
			product //= nums[l]
			l += 1

		res += r-l+1

	return res
```
