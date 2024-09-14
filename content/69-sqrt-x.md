---
type: leetcode
title: 69. sqrt(x)
tags:
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-02
updated: 2024-09-02
---

Given a non-negative integer `x`, return _the square root of_ `x` _rounded down to the nearest integer_. The returned integer should be **non-negative** as well.

You **must not use** any built-in exponent function or operator.

- For example, do not use `pow(x, 0.5)` in c++ or `x ** 0.5` in python.

## solution

Binary search for the value, kind of like [[875-koko-eating-bananas]].

```python
def mySqrt(self, x: int) -> int:
	# add 1 to r to account for edge case x=1
	l, r = 0, x // 2 + 1
	  
	# bisect_left would insert 2.8 at index 3, but we round down
	# so subtract 1 if not exact match
	while l < r:
		m = (l+r)//2
	  
		if m*m >= x:
			r = m
		else:
			l = m+1
	  
	return l if l*l == x else l-1
```
