---
type: leetcode
title: 75. sort colors
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/sort-colors/
date: 2022-11-21
updated: 2024-09-01
---

Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

## solution

The easy solution is just to count up the frequencies and overwrite the array.

However, to do it in one-pass, we need to know the trick. We sort in-place by keeping track of where we are with putting zeroes in the front and twos in the back.

```python
def sortColors(self, nums: List[int]) -> None:
	n = len(nums)
	p0, p2 = 0, n-1
	  
	i = 0
	while i <= p2:
		if nums[i] == 0:
			nums[i], nums[p0] = nums[p0], nums[i]

			# make sure p0 doesn't go ahead of i
			if p0 == i:
				i += 1

			p0 += 1
		elif nums[i] == 1:
			i += 1
		else:
			nums[i], nums[p2] = nums[p2], nums[i]
			p2 -= 1
```
