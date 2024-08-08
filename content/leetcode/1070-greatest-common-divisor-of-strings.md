---
type: leetcode
title: 1070. greatest common divisor of strings
tags:
  - math
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-06
updated: 2024-07-06
---

For two strings `s` and `t`, we say "`t` divides `s`" if and only if `s = t + t + t + ... + t + t` (i.e., `t` is concatenated with itself one or more times).

Given two strings `str1` and `str2`, return _the largest string_ `x` _such that_ `x` _divides both_ `str1` _and_ `str2`.

## solution

### brute force

We test every prefix until we reach the length of the shorter string.

```python
def gcdOfStrings(self, str1: str, str2: str) -> str:
	ans = ""
	acc = ""
	  
	def check(t):
		l1, l2, lt = len(str1), len(str2), len(t)
		if l1 % lt == 0 and l2 % lt == 0:
			if t*(l1//lt) == str1 and t*(l2//lt) == str2:
				return True
		return False
	  
	# str2 is always shorter
	if len(str2) > len(str1):
		str1, str2 = str2, str1
	  
	while True:
		if len(acc) == len(str1):
			break

		new_char = str1[len(acc)]
		acc += new_char
	  
		if len(acc) > len(str2):
			break
		if str1[:len(acc)] != acc or str2[:len(acc)] != acc:
			break
	  
		if check(acc):
			ans = acc

	return ans
```

### clever math

Realize that if the concatenation of the two strings is the same in both orientations, then they have a valid answer.

Just find the GCD of their lengths if they do.

```python
def gcdOfStrings(self, str1: str, str2: str) -> str:
	# Check if they have non-zero GCD string.
	if str1 + str2 != str2 + str1:
		return ""
	
	# Get the GCD of the two lengths.
	max_length = gcd(len(str1), len(str2))
		return str1[:max_length]
```
