---
type: leetcode
title: 214. shortest palindrome
tags:
  - kmp
  - palindrome
  - two-pointer
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-12
updated: 2024-10-12
---

You are given a string `s`. You can convert `s` to a  palindrome
 by adding characters in front of it.

Return _the shortest palindrome you can find by performing this transformation_.

## solutions

### find longest prefix palindrome

```python
# O(n^2)
def shortestPalindrome(self, s: str) -> str:
	"""
	maximally, we add n-1 characters
	(to create odd length palindrome)
	  
	the best case is it's already a palindrome
	starting from normal 1 and 2 centers, expand outwards
	  
	if not palindrome, shift center leftward and try again
	  
	(this is n^2??)
	  
	xxxabcd
	  
	find the longest palindrome starting at i=0,
	and just prepend the reversed remainder
	"""
	n = len(s)
	  
	def is_valid_palindrome(l, r):
		while l < r:
			if s[l] != s[r]:
				return False
			l += 1
			r -= 1
		return True

	for i in reversed(range(len(s))):
		if is_valid_palindrome(0, i):
			if i == n-1:
				return s
			return s[i+1:][::-1]+s
	return ""
```

### knuth-morris pratt

TODO
