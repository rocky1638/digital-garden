---
type: concept
title: "binary search"
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-05-30
---

## leetcode tips

Try to always start from a base of using the equivalent of `bisect_left` or `bisect_right`, as it has some more useful additional properties compared to any arbitrary implementation of binary search.

```python
###############
# bisect_left #
###############

def search(self, nums: List[int], target: int) -> int:
	l,r = 0, len(nums)-1

	while l < r:
		m = (l+r) // 2

		if nums[m] < target:
			l = m+1
		else:
			r = m

	return l

################
# bisect_right #
################

def search(self, nums: List[int], target: int) -> int:
	l,r = 0, len(nums)-1

	while l < r:
		m = (l+r) // 2

		if nums[m] > target:
			r = m
		else:
			l = m+1

	return l
```

`bisect_left` will always return the index of the first of occurrence of the target if it exists, and the index where it should be inserted if it does not exist.

`bisect_right` will always return the index after all of the existing targets if target exists in the array, and the index to insert if it does not exist.

Notice that `bisect_right` simply flips the `r=m` and `l=m+1` assignments. The difference in behavior comes from how the `nums[m] == target` case is handled.

## references

- https://www.piratekingdom.com/leetcode/tricks/leftmost-binary-search
