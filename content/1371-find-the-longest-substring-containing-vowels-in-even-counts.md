---
type: leetcode
title: 1371. find the longest substring containing vowels in even counts
tags:
  - bitmask
  - hashmap
  - prefix-sums
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-09-21
---

Given the string `s`, return the size of the longest substring containing each vowel an even number of times. That is, 'a', 'e', 'i', 'o', and 'u' must appear an even number of times.

## solution

The intuition here is very similar to [[523-continuous-subarray-sum]], where we iterate through the list while keeping track of the parity of each vowels’ frequency.

If the current parity is equal to a previous parity, then that means the substring in between has even counts for every vowel!

```python
def findTheLongestSubstring(self, s: str) -> int:
	vowels = "aeiou"
	# prefix counts
	leftmost_bitmask = {"00000": -1}
	res = 0
	
	bitmask = [0,0,0,0,0]
	for i in range(len(s)):
		if s[i] in vowels:
			# update running bitmask
			bitmask[vowels.index(s[i])] ^= 1
	
		current_bitmask = "".join(map(str, bitmask))
		if current_bitmask in leftmost_bitmask:
			res = max(res, i-leftmost_bitmask[current_bitmask])
		else:
			leftmost_bitmask[current_bitmask] = i
	
	return res
```

Instead of using string bitmask and constantly converting between list and string, we use an actual bitmask integer.

```python
def findTheLongestSubstring(self, s: str) -> int:
	vowels = "aeiou"
	# prefix counts
	leftmost_bitmask = {0: -1}
	res = 0
	  
	bitmask = 0
	for i in range(len(s)):
		if s[i] in vowels:
			# update running bitmask
			# target the correct bit by left shifting
			bitmask ^= 1 << vowels.index(s[i])

		if bitmask in leftmost_bitmask:
			res = max(res, i-leftmost_bitmask[bitmask])
		else:
			leftmost_bitmask[bitmask] = i
	return res
```
