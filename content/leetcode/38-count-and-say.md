---
type: leetcode
title: 38. count and say
tags:
  - recursion
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-31
---

The **count-and-say** sequence is a sequence of digit strings defined by the recursive formula:

- `countAndSay(1) = "1"`
- `countAndSay(n)` is the run-length encoding of `countAndSay(n - 1)`.

[Run-length encoding](http://en.wikipedia.org/wiki/Run-length_encoding) (RLE) is a string compression method that works by replacing consecutive identical characters (repeated 2 or more times) with the concatenation of the character and the number marking the count of the characters (length of the run). For example, to compress the string `"3322251"` we replace `"33"` with `"23"`, replace `"222"` with `"32"`, replace `"5"` with `"15"` and replace `"1"` with `"11"`. Thus the compressed string becomes `"23321511"`.

Given a positive integer `n`, return _the_ `nth` _element of the **count-and-say** sequence_.

## solutions

### recursive

```python
class Solution:
	def rle(self, s):
		res = []
		count = 1
	  
		for i in range(1, len(s)):
			if s[i] == s[i - 1]:
				count += 1
			else:
				res.append(f"{count}{s[i - 1]}")
				count = 1
		res.append(f"{count}{s[-1]}")
	  
		return "".join(res)
	  
	def countAndSay(self, n: int) -> str:
		if n == 1:
			return "1"
		return self.rle(self.countAndSay(n-1))
```

### iterative

```python
class Solution:
	def rle(self, s):
		res = []
		count = 1
	  
		for i in range(1, len(s)):
			if s[i] == s[i - 1]:
				count += 1
			else:
				res.append(f"{count}{s[i - 1]}")
				count = 1
		res.append(f"{count}{s[-1]}")
	  
		return "".join(res)
	  
	
	def countAndSay(self, n: int) -> str:
		res = "1"
		for i in range(n-1):
			res = self.rle(res)
		return res
```
