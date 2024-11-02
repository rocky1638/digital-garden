---
type: leetcode
title: 453. minimum moves to equal array elements
tags:
  - math
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-22
updated: 2024-10-22
---

Given an integer array `nums` of size `n`, return _the minimum number of moves required to make all array elements equal_.

In one move, you can increment `n - 1` elements of the array by `1`.

## solution

Incrementing $n-1$ items is logically equivalent to decrementing a single item, which simplifies this problem greatly.

```python
# O(n)
def minMoves(self, nums: List[int]) -> int:
	"""
	[2,3,3,3]
	=> [3,4,4,3] OR [2,3,3,2]
	=> [4,5,4,4] OR [2,3,2,2]
	=> [5,5,5,5] OR [2,2,2,2]
	  
	incrementing n-1 nums is logically equivalent to decrementing one num!
	"""
	minimum = min(nums)
	res = 0
	  
	for num in nums:
		res += num-minimum
	return res
```
