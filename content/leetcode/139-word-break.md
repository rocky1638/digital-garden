---
type: leetcode
title: 139. word break
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/word-break/
date: 2022-11-17
updated: 2024-08-17
tags:
  - dp
  - string
---

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

## solutions

### recursion w/ memoization

At each recursive step, choose to split the string at `idx`, or continue accumulating a string.

```python
def wordBreak(self, s: str, wordDict: List[str]) -> bool:
	word_set = set(wordDict)
	memo = {}

	def recurse(idx, wl):
		if idx == len(s) and wl == len(s):
			return True
		if idx == len(s) or wl == len(s):
			return False

		if (idx, wl) in memo:
			return memo[(idx, wl)]
	
		# if wl to idx forms word in list,
		# choose to either split with it or not
		splittable = False
		window_word = s[wl:idx+1]

		# choose to split here, start next
		# word in recursion
		if window_word in word_set:
			splittable = splittable or recurse(idx+1, idx+1)
		  
		# don't split here, continue to next index
		splittable = splittable or recurse(idx+1, wl)
		  
		memo[(idx, wl)] = splittable
		return splittable
	  
	return recurse(0, 0)
```

### dp

Instead of top-down recursion, we can build the solution bottom-up by starting with the empty string, and adding characters. For any given string ending at $i$, we look back at all prior indices $j$ where the string was splittable, and see if the string `s[j:i+1]` is valid.

```python
def wordBreak(self, s: str, wordDict: List[str]) -> bool:
	word_set = set(wordDict)
	  
	dp = [True]
	for i in range(len(s)):
		j = i
		dp.append(False)
		while j >= 0:
			if dp[j] and s[j:i+1] in word_set:
				dp[-1] = True
				break
			j -= 1
	return dp[-1]
```
