---
type: leetcode
title: 791. custom sort string
tags:
  - sorting
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-31
---

You are given two strings `order` and `s`. All the characters of `order` are **unique** and were sorted in some custom order previously.

Permute the characters of `s` so that they match the order that `order` was sorted. More specifically, if a character `x` occurs before a character `y` in `order`, then `x` should occur before `y` in the permuted string.

Return _any permutation of_ `s` _that satisfies this property_.

## solutions

### custom comparator

Map the characters in `order` to indices to use that as custom comparator.

```python
def customSortString(self, order: str, s: str) -> str:
	a = list(s)
	  
	# put unknown characters to the end
	char_to_idx = defaultdict(lambda: 26)
	for i, char in enumerate(order):
		char_to_idx[char] = i
	  
	def merge(arr1, arr2):
		p1, p2 = 0, 0
		res = []
		while p1 < len(arr1) and p2 < len(arr2):
			if char_to_idx[arr1[p1]] < char_to_idx[arr2[p2]]:
				res.append(arr1[p1])
				p1 += 1
			else:
				res.append(arr2[p2])
				p2 += 1
	  
		while p1 < len(arr1):
			res.append(arr1[p1])
			p1 += 1
		while p2 < len(arr2):
			res.append(arr2[p2])
			p2 += 1
		return res
	  
	def merge_sort(arr):
		if len(arr) == 1:
			return arr
		if len(arr) == 2:
			# out of order, swap
			if char_to_idx[arr[0]] > char_to_idx[arr[1]]:
				arr = arr[::-1]
			return arr
		else:
			m = len(arr)//2
			left_half = merge_sort(arr[:m])
			right_half = merge_sort(arr[m:])
			return merge(left_half, right_half)
	return "".join(merge_sort(a))
```

### hashmap string construction

We can just put all the characters from `s` into a hashmap, and iterate through order. Once we see a character that exists in `s`, add to final string.
