---
type: leetcode
title: 670. maximum swap
tags:
  - greedy
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-30
updated: 2024-08-30
---

You are given an integer `num`. You can swap two digits at most once to get the maximum valued number.

Return _the maximum valued number you can get_.

## solution

Construct a map that stores the right most index of each digit!

```python
def maximumSwap(self, num: int) -> int:
	"""
	fully descending - no larger number

	first digit from right that has larger digit to the right
	should be swapped with the rightmost instance of the largest
	of those digits.
	"""
	sn = list(str(num))
	last_seen = [-1]*10
	  
	for i, digit in enumerate(sn):
		last_seen[int(digit)] = i
	  
	# iterate from left of num
	for i, digit in enumerate(sn):
		# check for digits larger than the digit
		# from 9 -> digit+1
		for j in reversed(range(int(digit)+1, 10)):
			if last_seen[j] > -1 and last_seen[j] > i:
				sn[i], sn[last_seen[j]] = sn[last_seen[j]], sn[i]
				return int("".join(sn))
	return num
```
