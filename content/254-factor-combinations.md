---
type: leetcode
title: 254. factor combinations
tags:
  - backtracking
  - math
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-13
---

Numbers can be regarded as the product of their factors.

- For example, `8 = 2 x 2 x 2 = 2 x 4`.

Given an integer `n`, return _all possible combinations of its factors_. You may return the answer in **any order**.

**Note** that the factors should be in the range `[2, n - 1]`.

## solutions

From the outset, it’s pretty obvious that this question involves some sort of backtracking.

### divide until 1

My initial instinct was to keep a list of factors, and keep trying to divide by factors until we divide down to 1. To avoid duplicates, we also pass in the factor that we’re on in the DFS, so our finished factor sets are non-decreasing.

```python
def getFactors(self, n: int) -> List[List[int]]:
	if n == 1:
		return []
	  
	factors = [k for k in range(2, n) if n%k == 0]
	  
	res = []
	acc = []
	def dfs(remaining, idx):
		if remaining == 1:
			res.append(acc[:])
			return
		for i, num in enumerate(factors[idx:]):
			if remaining % num == 0:
				acc.append(num)
				dfs(remaining // num, i+idx)
				acc.pop()
	dfs(n, 0)
	return res
```

### optimized - store intermediate paths

Trying to optimize duplicated work is actually quite tricky here. We realize that for an example like $n=12$. We can decide to divide by $2$, leaving us with an `acc` of `[2]` and a remaining value of $6$. We can continue down this recursion, ultimately getting a factor set of `[2,2,3]`.

Within that same loop at `[2]`, we will also recurse towards `[2,6]`, which we’ll separately add to the answer set.

The observation is that within our recursive call, we could’ve just saved `[2,6]`. Essentially, as we divide by values, we can just save the intermediate steps as output as well, instead of explicitly recursing directly to those values.

```python
def getFactors(self, n: int) -> List[List[int]]:
	output = []
	end = int(math.sqrt(n))+1
	
	def backtrack(val, start, path):
		if path:
			output.append(path + [val])
		for i in range(start, end):
			if val % i == 0:
				backtrack(val//i, i, path + [i])
	
	backtrack(n, 2, [])
	return output
```
