---
type: leetcode
title: 633. sum of square numbers
tags:
  - two-pointer
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-01
updated: 2024-09-01
---

Given a non-negative integer `c`, decide whether there're two integers `a` and `b` such that `a2 + b2 = c`.

## solutions

### set

```python
def judgeSquareSum(self, c: int) -> bool:
	if c == 0:
		return True
  
	squares = set([0])
	for v in range(1, int(sqrt(c))+1):
		val1 = v**2
		squares.add(val1)
		if c-val1 in squares:
			return True
	return False
```

### two pointers

```python
def judgeSquareSum(self, c: int) -> bool:
	r = int(c**0.5)
	  
	if r*r == c:
		return True
	  
	l = 1
	while l <= r:
		cand = l*l+r*r
		if cand == c:
			return True
		elif cand < c:
			l +=1
		else:
			r -= 1
	return False
```
