---
type: leetcode
title: 274. h-index
tags:
  - binary-search
  - counting-sort
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-14
updated: 2024-10-14
---

Given an array of integers `citations` where `citations[i]` is the number of citations a researcher received for their `ith` paper, return _the researcher's h-index_.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): The h-index is defined as the maximum value of `h` such that the given researcher has published at least `h` papers that have each been cited at least `h` times.

## solutions

### binary search

We can binary search on the possible answers, and use $O(n)$ time to calculate if a given h-index is valid.

```python
def hIndex(self, citations: List[int]) -> int:
	def check(h):
		count = 0
		for cite in citations:
			if cite >= h:
				count += 1
		return count >= h

	l, r = 0, len(citations)
	  
	while l <= r:
		m = (l+r)//2
		if check(m) and (m == len(citations) or not check(m+1)):
			return m
		elif check(m):
			l = m+1
		else:
			r = m-1
```

### counting sort

We can achieve linear time by first creating a sorted frequency list.

Note that we want to iterate through the frequency list in reverse, because that way we can maintain an accumulator of all the papers that satisfy the condition of $\ge i$ citations at any index $i$.

Then, if at any point our count of papers is $\ge$ the current h-index (`i` in this case), we can just return it as that is the biggest h-index we could achieve.

```python
def hIndex(self, citations: List[int]) -> int:
	n = max(citations)
	counts = [0]*(n+1)
	  
	# populate sorted frequency list
	for cite in citations:
		counts[cite] += 1

	acc = 0
	for i in reversed(range(n+1)):
		acc += counts[i]
	  
		if acc >= i:
			return i
```
