---
type: leetcode
title: 186. reverse words in a string ii
tags:
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-11
---

Given a character array `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by a single space.

Your code must solve the problem **in-place,** i.e. without allocating extra space.

## solution

We have to somehow get the words to the other side of the sentence. Instead of thinking about flipping individual characters at first, just flip the whole word so the order is reversed, then individually flip each word again.

```python
def reverseWords(self, s: List[str]) -> None:
	def flip_range(l, r):
		while l < r:
			s[l], s[r] = s[r], s[l]
			l += 1
			r -= 1
	  
	n = len(s)
	  
	# flip entire string
	flip_range(0, n-1)
	  
	# flip each word in string
	l = r = 0
	while r < n:
		if s[r] == " ":
			flip_range(l, r-1)
			l = r+1
			r += 1
		else:
			r += 1
	flip_range(l, r-1)
```
