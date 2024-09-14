---
type: leetcode
title: 291. word pattern ii
tags:
  - backtracking
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-15
updated: 2024-08-26
---

Given a `pattern` and a string `s`, return `true` _if_ `s` _**matches** the_ `pattern`_._

A string `s` **matches** a `pattern` if there is some **bijective mapping** of single characters to **non-empty** strings such that if each character in `pattern` is replaced by the string it maps to, then the resulting string is `s`. A **bijective mapping** means that no two characters map to the same string, and no character maps to two different strings.

## solution

When first seeing the problem, it’s pretty clear that we want to do some sort of backtracking to enumerate the possible mappings.

Like normal, we can keep track of a dictionary to map pattern chars to strings, and then add/remove them when we enter/return from recursion.

The only slightly tricky thing here is the third recursion element, which keeps track of the left bound of the active “window” we’re considering for the next string.

```python
def wordPatternMatch(self, pattern: str, s: str) -> bool:
	mappings = {}
	mapped_strs = set()
	  
	def recurse(idx, map_idx, wl):
		if map_idx == len(pattern) and idx == len(s):
			return True
		if map_idx == len(pattern) or idx == len(s):
			return False
	  
		# if mapping exists, check if string[idx:idx+map_len] matches mapping
		if pattern[map_idx] in mappings:
			mapped = mappings[pattern[map_idx]]
			# if so, advance idx, map_idx, pat_l = pat_r =
			if s[idx:idx+len(mapped)] == mapped:
				return recurse(idx+len(mapped), map_idx+1, idx+len(mapped))
			# if not, return False
			else:
				return False

		# either take current acc as map for pattern[map_idx] or continue
		  
		# make current window into mapping
		mapped = s[wl:idx+1]
		use_current = False
		if mapped not in mapped_strs:
			mappings[pattern[map_idx]] = mapped
			mapped_strs.add(mapped)
			use_current = recurse(idx+1, map_idx+1, idx+1)
			mapped_strs.remove(mapped)
			del mappings[pattern[map_idx]]
	
		# continue expanding window
		cont = recurse(idx+1, map_idx, wl)
		  
		return use_current or cont
	  
	return recurse(0, 0, 0)
```

Here’s another solution without using the third recursion parameter of `wl`, but instead we just iterate through each possible mapping for the next pattern character.

```python
def wordPatternMatch(self, pattern: str, s: str) -> bool:
	mappings = {}
	mapped_strs = set()
	  
	def recurse(idx, map_idx):
		if map_idx == len(pattern) and idx == len(s):
			return True
		if map_idx == len(pattern) or idx == len(s):
			return False
	  
		# if mapping exists, check if string[idx:idx+map_len] matches mapping
		if pattern[map_idx] in mappings:
			mapped = mappings[pattern[map_idx]]
			# if so, advance idx, map_idx
			if s[idx:idx+len(mapped)] == mapped:
				return recurse(idx+len(mapped), map_idx+1)
			# if not, return False
			else:
				return False

		# try mapping each string from idx to end as next pattern
		valid = False
		for i in range(idx+1, len(s)+1):
			sub = s[idx:i]

			if sub in mapped_strs:
				continue
		  
			mappings[pattern[map_idx]] = sub
			mapped_strs.add(sub)
			valid = valid or recurse(i, map_idx+1)
			mapped_strs.remove(sub)
			del mappings[pattern[map_idx]]

		return valid
	  
	return recurse(0, 0)
```
