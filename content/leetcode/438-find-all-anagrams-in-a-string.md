---
type: leetcode
title: 438. find all anagrams in a string
date: 2022-11-23
updated: 2024-09-14
tags:
  - sliding-window
  - hashmap
---

Given two strings `s` and `p`, return _an array of all the start indices of_ `p`_'s anagrams in_ `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## solutions

### hashmap

- classic [[sliding-window]] problem using a [[frequency-map]].
- when the [[frequency-map]] of the string `p` matches with the frequency of the window we’re looking at in `s`, we add the index to the `ans` array.

```python
def findAnagrams(self, s: str, p: str) -> List[int]:
	freq = Counter(s[:len(p)])
	pfreq = Counter(p)
	
	ans = []
	
	if freq == pfreq:
		ans.append(0)
	
	for i in range(1, len(s)-len(p)+1):
		freq[s[i-1]] -= 1
		freq[s[i+len(p)-1]] += 1
	
		if freq == pfreq:
			ans.append(i)
	return ans
```

### fixed size buckets

Instead of incurring the overhead of hashmaps, we can just use a fixed length array to track frequencies.

```python
def findAnagrams(self, s: str, p: str) -> List[int]:
	window_counter = [0]*26
	p_counter = [0]*26
	for char in p:
		p_counter[ord(char)-97] += 1
	  
	res = []
	l = 0
	for r in range(len(s)):
		char_idx = ord(s[r])-97
		window_counter[char_idx] += 1

		if (r-l+1) > len(p):
			char_idx = ord(s[l])-97
			window_counter[char_idx] -= 1
			l += 1

		if window_counter == p_counter:
			res.append(l)
	return res
```
