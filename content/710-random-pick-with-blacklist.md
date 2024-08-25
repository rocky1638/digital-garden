---
type: leetcode
title: 710. random pick with blacklist
tags:
  - hashmap
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-23
updated: 2024-08-23
---

You are given an integer `n` and an array of **unique** integers `blacklist`. Design an algorithm to pick a random integer in the range `[0, n - 1]` that is **not** in `blacklist`. Any integer that is in the mentioned range and not in `blacklist` should be **equally likely** to be returned.

Optimize your algorithm such that it minimizes the number of calls to the **built-in** random function of your language.

Implement the `Solution` class:

- `Solution(int n, int[] blacklist)` Initializes the object with the integer `n` and the blacklisted integers `blacklist`.
- `int pick()` Returns a random integer in the range `[0, n - 1]` and not in `blacklist`.

## solution

Some intuition is required:

1. We want to use something like `random.randint()`, but this requires a contiguous range. We have random blacklist numbers within our range $[0, n-1]$.
2. We actually only want a random value for the number of whitelisted values we have, not all of $n$.

If we have $n$ values with $b$ blacklisted values and $w = n-b$ whitelisted values, we want to generate a random number in the range $[0, w-1]$. If there’s blacklisted values in this range, there will be an equal number of whitelisted values in the range $[w, n-1]$. We can use a hashmap to map each of these blacklisted values in the whitelist range to whitelisted values in the blacklist range.

After that is done, we can just generate a random number in the range $[0, w-1]$, and return the mapped value if we happen to generate a blacklisted value!

```python
class Solution:
	def __init__(self, n: int, blacklist: List[int]):
		self.whitelist_size = n-len(blacklist)
		self.blacklist_set = set(blacklist)
		self.blacklist_map = {}
		  
		# map all blacklisted items to tail of range
		idx = n-1
		for b in blacklist:
			# blacklisted value already in tail
			if b >= self.whitelist_size:
				continue

			# iterate to next whitelisted value
			while idx in self.blacklist_set:
				idx -= 1

			self.blacklist_map[b] = idx
			idx -= 1
	  
	def pick(self) -> int:
		idx = random.randint(0, self.whitelist_size-1)
		if idx in self.blacklist_map:
			return self.blacklist_map[idx]
		return idx
```
