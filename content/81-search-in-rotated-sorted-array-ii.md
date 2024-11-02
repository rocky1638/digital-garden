---
type: leetcode
title: 81. search in rotated sorted array ii
tags:
  - binary-search
aliases: 
parents:
  - "[[33-search-in-rotated-sorted-array]]"
children: 
supports: 
enemies: 
date: 2024-10-23
updated: 2024-10-23
---

There is an integer array `nums` sorted in non-decreasing order (not necessarily with **distinct** values).

Before being passed to your function, `nums` is **rotated** at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,4,4,5,6,6,7]` might be rotated at pivot index `5` and become `[4,5,6,6,7,0,1,2,4,4]`.

Given the array `nums` **after** the rotation and an integer `target`, return `true` _if_ `target` _is in_ `nums`_, or_ `false` _if it is not in_ `nums`_._

You must decrease the overall operation steps as much as possible.

## solution

For any given `m` value, the pivot will sit on either the left or right. We should make our determination of where to split by using the side that _doesn’t_ have the pivot (in other words, is properly sorted).

We can handle duplicates by special casing when `nums[l] == nums[m] == nums[r]`. In this case, we can’t determine which side is sorted, and we also know none of those values are `target`. So, we can move `l` and `r` inwards.

```python
def search(self, nums: List[int], target: int) -> bool:
	l, r = 0, len(nums)-1
	while l <= r:
		m = (l+r)//2
	  
		if nums[m] == target:
			return True
	  
		# we can't determine which side is sorted
		if nums[l] == nums[m] == nums[r]:
			l += 1
			r -= 1
	  
		# [l:m] is sorted, check it
		elif nums[l] <= nums[m]:
			# it's in the left half, remove right half
			if nums[l] <= target <= nums[m]:
				r = m-1
			else: # it's not in left half, look in right half
				l = m+1
		# [l:m] is rotated, binary search on [m:r]
		else:
			# target is in right half, omit left
			if nums[m] <= target <= nums[r]:
				l = m+1
			else:
				r = m-1
	return False
```
