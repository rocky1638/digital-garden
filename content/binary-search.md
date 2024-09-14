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
updated: 2024-08-31
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

		if nums[m] <= target:
			l = m+1
		else:
			r = m

	return l
```

`bisect_left` will always return the index of the first of occurrence of the target if it exists, and the index where it should be inserted if it does not exist.

`bisect_right` will always return the index after all of the existing targets if target exists in the array, and the index to insert if it does not exist.

Notice the only difference between `bisect_left` and `bisect_right` is how the “equals” case is handled. In `bisect_left`, `l` doesn’t move and `r` moves down if the value equals. This means that `l` will stay on the left of block of equals values.

For `bisect_right`, `l` moves right even on equals, meaning it’ll move past all of the values that are equal to our `target` and end up on the right of them.

## template for “find leftmost that satisfies condition”

```python
def binsearch():
	l, r = 0, len(arr)
	
	while l < r:
		m = l+(r-l)//2

		if condition(arr[m]):
			r = m
		else:
			l = m+1
	# l is at the index of leftmost value that satisfies condition
	return l	 
```

The intuition here is that if our current `m` satisfies the condition, we move `r` to `m` (and not `m-1`), because `m` might be the leftmost satisfying value.

On the contrary, if `m` doesn’t satisfy, then we can safely move past it, and set `l=m+1`.

We set `r` to `len(arr)` and not `len(arr)-1` because there could be the case where no values satisfy the condition, in which case we return `len(arr)` which we can interpret as a failure.

## references

- https://www.piratekingdom.com/leetcode/tricks/leftmost-binary-search
- https://leetcode.com/problems/koko-eating-bananas/solutions/769702/python-clear-explanation-powerful-ultimate-binary-search-template-solved-many-problems
