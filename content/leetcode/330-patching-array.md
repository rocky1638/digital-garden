---
type: leetcode
title: 330. patching array
tags:
  - greedy
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-09
updated: 2024-08-09
---

Given a sorted integer array `nums` and an integer `n`, add/patch elements to the array such that any number in the range `[1, n]` inclusive can be formed by the sum of some elements in the array.

Return _the minimum number of patches required_.

## solution

Several intuitions and insights are required.

- Initially, the range that we cover is an empty range.
- We need a $1$ in the array to cover the value of $1$. Our `next_oob` value is $2$.
- If we see the next value in our array is smaller than or equal to the `next_oob` value, we know that our range can expand by this value.
	- To prove this, imagine that after some values in `nums`, our covered range is $[1, j]$. If we see any value $k$ that is $\le j$, we know that any sum $[1,j]$ can be constructed with the values before $k$, and $k$ can be added to any value in that range. Therefore, our new range is expanded to $[1,k+j]$.
- If the next value in `nums` is larger than `next_oob`, we know that we will need to patch.
	- e.g. Consider `nums=[1,2,3,8]`. After `[1,2,3]`, our covered range is $[1,6]$, but we have a hole where we don’t cover $7$.
	- To cover $7$, we have to patch with some value that is $\le 7$. With similar logic as above, we can greedily patch with $7$ and not a smaller value, because patching with $7$ will increase our covered range the most (to $[1, 6+7]$).

```python
def minPatches(self, nums: List[int], n: int) -> int:
	"""
	1 -> covered range: [1, 1]
	1, 2 -> covered range: [1, 3]
	# if new number is in existing coverage range,
	# just extend range by the new value
	1, 2, 3 -> covered range: [1, 6]
	# we need a patch here, because 7 > previous range upper 6
	1, 2, 3, 8 -> covered range: [1, 6], [8, 14]
	1, 2, 100 -> [1,3], [100,103]
	add 4 -> [1,7], [100,107]
	"""
	next_oob = 1
	patches = 0

	i = 0
	while next_oob <= n:
		# gone through original values
		# keep adding patches until we reach n
		if i == len(nums):
			patches += 1
			next_oob *= 2
		# next num already covered,
		# it just increases our coverage
		elif nums[i] <= next_oob:
			next_oob += nums[i]
			i += 1
		# nums[i] is out of coverage, we patch
		# with next_oob to increase range to [1, next_oob*2]
		else:
			patches += 1
			next_oob *= 2

return patches
```
