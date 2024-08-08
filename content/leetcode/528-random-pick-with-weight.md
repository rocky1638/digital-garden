---
date: 2022-12-25
updated: 2024-08-07
type: leetcode
title: 528. random pick with weight
tags:
  - binary-search
  - array
  - prefix-sums
---

You are given a **0-indexed** array of positive integers `w` where `w[i]` describes the **weight** of the `ith` index.

You need to implement the function `pickIndex()`, which **randomly** picks an index in the range `[0, w.length - 1]` (**inclusive**) and returns it. The **probability** of picking an index `i` is `w[i] / sum(w)`.

- For example, if `w = [1, 3]`, the probability of picking index `0` is `1 / (1 + 3) = 0.25` (i.e., `25%`), and the probability of picking index `1` is `3 / (1 + 3) = 0.75` (i.e., `75%`).

## solutions

### prefix sums + binary search

We store the upper bounds of each index’s weight range in the array, in a similar idea to prefix sum.

Then, we can generate a random number in the range of the total weight of the array, and find the “weight bucket” that the number fits into. We can find this index by doing binary search, for the largest number that is smaller than `target`.

```python
class Solution:
	def __init__(self, w: List[int]):
		# in array, store upper bound of cumulative weight
		self.a = []
		
		tally = 0
		for weight in w:
			tally += weight
			self.a.append(tally)
		self.total = tally
	
	def pickIndex(self) -> int:
		target = self.total * random.random()
		l, r = 0, len(self.a)
		while l < r:
			m = (l+r)//2
			if target > self.a[m]:
				l = m + 1
			else:
				r = m
		return l
```

Note, we can also do this using `bisect`. We use `self.total+1` because that brings our search into the range `[1, total]` instead of `[0, total-1]`.

```python
class Solution:
	def __init__(self, w: List[int]):
		self.prefixes = []
		self.total = 0
	  
		for weight in w:
			self.total += weight
			self.prefixes.append(self.total)
	  
	def pickIndex(self) -> int:
		v = random.randrange(self.total)+1
		return bisect_left(self.prefixes, v)
```
