---
type: leetcode
title: 137. single number ii
tags:
  - bit-manipulation
aliases: 
parents:
  - "[[136-single-number]]"
children: 
supports: 
enemies: 
date: 2024-10-09
updated: 2024-10-09
---

Given an integer array `nums` where every element appears **three times** except for one, which appears **exactly once**. _Find the single element and return it_.

You must implement a solution with a linear runtime complexity and use only constant extra space.

## solution

Unlike the solution for [[136-single-number]], we can’t just use a basic XOR here, but we do need to do some sort of bit manipulation.

The key intuition here is that instead of just XOR’ing every value and knowing that equal values will cancel each other out, we need two values to keep track of bits we’ve seen once and bits we’ve seen twice. We use the variables `ones` and `twos` for that.

For every number in `nums`, we essentially put the numbers bits into ones and twos.

- If a bit exists in `num` and already exists in `twos`, then we must remove that bit from `ones` and `twos` (using a bitwise XOR).
- If a bit exists in `ones` and not `twos`, we need to add it to `twos` (with a bitwise OR).

Note that after we remove the bits that already exist in `twos`, we only proceed to add the _other_ bits, which we get by doing a bitwise XOR between `num` and `already_in_twos`.

```python
def singleNumber(self, nums: List[int]) -> int:
	ones = 0
	twos = 0
	  
	for num in nums:
	# get values already set in twos
	# (to update twos)
	already_in_twos = twos & num
	  
	# ^ these bits need to be removed from ones and twos
	ones ^= already_in_twos
	twos ^= already_in_twos
	  
	# get the remaining bits of nums,
	# excluding the ones we removed from twos
	rem = num ^ already_in_twos
	  
	# we need to add these remaining bits to ones
	  
	# first, find which ones already exist in ones
	# these will need to be added to twos
	already_in_ones = rem & ones
	  
	# add the values already in ones to twos
	twos |= already_in_ones
	  
	# add non-cleared bits of nums to ones
	ones |= rem
	  
	return ones
```
