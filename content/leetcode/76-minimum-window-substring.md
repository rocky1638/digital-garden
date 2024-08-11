---
type: leetcode
title: 76. minimum window substring
aliases: 
difficulty: 🔴
link: https://leetcode.com/problems/minimum-window-substring/
date: 2022-11-24
updated: 2024-08-10
tags:
  - sliding-window
  - hashmap
  - string
---

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window _substring_** _of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window_. If there is no such substring, return _the empty string_ `""`.

The testcases will be generated such that the answer is **unique**.

## solution

### sliding window with two hashmaps

This is a classic [[sliding-window]] approach using [[frequency-map]].

We slide our right pointer over until we have a valid string, then try to shrink our window until it is invalid again.

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        tcount = Counter(t)
        wincount = Counter()
        l = 0
        ans = ""
        best = float("inf")
        
        # expand r forward until window is valid
        # then move l forward until invalid
        for r in range(len(s)):
            wincount[s[r]] += 1
            while all(wincount[x] >= tcount[x] for x in tcount):
                winlength = r-l+1
                if winlength < best:
                    ans = s[l:r+1]
                    best = len(ans)
                wincount[s[l]] -= 1
                l += 1
        return ans
```

### sliding window with $O(1)$ validation

The main optimization here is that instead of keeping two hashmaps and comparing them against each other, we just keep a single value that tracks how many unique letters we’ve matched.

We then simply have to make sure that the number of `matched` is equal to the number of unique letters in `t`.

```python
def minWindow(self, s: str, t: str) -> str:
	if len(t) > len(s):
	return ""

	wc = Counter()
	tc = Counter(t)
	matched = 0
	  
	ans = ""
	best_len = float("inf")
	l = 0
	for r in range(len(s)):
		wc[s[r]] += 1
		if wc[s[r]] == tc[s[r]]:
			matched += 1
	
		# while we've matched all the distinct
		# chars in t
		while matched == len(tc):
			if r-l+1 < best_len:
				best_len = r-l+1
				ans = s[l:r+1]
		
			wc[s[l]] -= 1
			if wc[s[l]] < tc[s[l]]:
				matched -= 1
			l += 1
	
	return ans
```
