---
type: leetcode
title: 231. power of two
tags:
  - bit-manipulation
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-18
updated: 2024-09-18
---

Given an integer `n`, return _`true` if it is a power of two. Otherwise, return `false`_.

An integer `n` is a power of two, if there exists an integer `x` such that `n == 2x`.

## solution

```python
def isPowerOfTwo(self, n: int) -> bool:
	# no negatives can be power of two
	# n = 10000
	# n-1 = 01111
	# n&(n-1) = 00000
	return n > 0 and n&(n-1) == 0
```
