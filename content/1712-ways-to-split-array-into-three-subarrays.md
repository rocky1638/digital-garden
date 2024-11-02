---
type: leetcode
title: 1712. ways to split array into three subarrays
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-19
updated: 2024-10-19
---

A split of an integer array is **good** if:

- The array is split into three **non-empty** contiguous subarrays - named `left`, `mid`, `right` respectively from left to right.
- The sum of the elements in `left` is less than or equal to the sum of the elements in `mid`, and the sum of the elements in `mid` is less than or equal to the sum of the elements in `right`.

Given `nums`, an array of **non-negative** integers, return _the number of **good** ways to split_ `nums`. As the number may be too large, return it **modulo** `109 + 7`.

## solutions

### backtracking + prefix sums

```python
# O(n^2)
def waysToSplit(self, nums: List[int]) -> int:
	# O(n)
	prefix_sums = [0]
	for num in nums:
		prefix_sums.append(prefix_sums[-1]+num)

	# O(1)
	def valid_split(idxs):
		if len(idxs) != 2:
			return False
		left = prefix_sums[idxs[0]+1]-prefix_sums[0]
		mid = prefix_sums[idxs[1]+1]-prefix_sums[idxs[0]+1]
		right = prefix_sums[-1]-prefix_sums[idxs[1]+1]
		return left <= mid <= right

	split_ids = []
	def recurse(idx):
		if idx == len(nums) or len(split_ids) == 2:
			if valid_split(split_ids):
				return 1
			return 0
	  
		ways = 0
		for i in range(idx, len(nums)):
			split_ids.append(i)
			ways += recurse(i+1)
			split_ids.pop()
		return ways % (10**9+7)

	return recurse(0)
```
