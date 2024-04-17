---
type: leetcode
title: "66. plus one"
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-03-29
---

You are given a **large integer** represented as an integer array `digits`, where each `digits[i]` is the `ith` digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading `0`'s.

Increment the large integer by one and return _the resulting array of digits_.

## solutions

This is the manual addition solution.

```python
def plusOne(self, digits: List[int]) -> List[int]:
	carry = 1
	ptr = len(digits)-1
	  
	while ptr >= 0:
		if carry == 0:
			break
		if carry == 1:
			digits[ptr] += 1
	  
		if digits[ptr] > 9:
			digits[ptr] -= 10
			carry = 1
		else:
			carry = 0
	  
		ptr -= 1

	# edge case for something like 99
	if carry == 1:
		digits = [1] + digits
	
	return digits
```

> [!tip]
> We could also just convert the digits to an `int`, add 1, and then convert it back to a list of digits.
