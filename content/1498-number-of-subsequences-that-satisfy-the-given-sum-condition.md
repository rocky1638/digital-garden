---
type: leetcode
title: 1498. number of subsequences that satisfy the given sum condition
tags:
  - sorting
  - binary-search
  - two-pointer
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-11-01
updated: 2024-11-01
---

Return _the number of **non-empty** subsequences of_ `nums` _such that the sum of the minimum and maximum element on it is less or equal to_ `target`. Since the answer may be too large, return it **modulo** `10^9 + 7`.

## solutions

The first big intuition is that this question isn’t really asking for subsequences, but just subsets. We don’t care about the ordering of the subsequences.

### enumeration

The most straightforward approach is to realize that this problem is simply just picking to skip/take each value. We can enumerate this using recursion.

```python
# O(2^n)
def numSubseq(self, nums: List[int], target: int) -> int:
	res = 0
	def recurse(idx, mn, mx):
		nonlocal res
		if idx == len(nums):
			if mn is not inf and mx+mn <= target:
				res += 1
			return
	  
		# take
		recurse(idx+1, min(mn, nums[idx]), max(mx, nums[idx]))
	  
		# skip
		recurse(idx+1, mn, mx)
	  
	recurse(0, inf, -inf)
	return res
```

### sorting + nested loop

Because we don’t care about the original ordering of `nums`, we can sort, and then do iterations as follows:
1. Pick `i` as the minimum value of a subsequence.
2. Find the largest value `j` such that `nums[j]` being the maximum satisfies the condition `nums[i]+nums[j] <= target`.
3. We know that we must include `nums[i]` in these subsets, but we can choose to take/skip each of the remaining values in `[i+1, j]`. This comes out to $2^{j+i}$.

```python
# O(n^2) worst case for the nested loop
def numSubseq(self, nums: List[int], target: int) -> int:
	res = 0
	nums.sort()

	for i in range(len(nums)):
		mn = nums[i]
		for j in reversed(range(i, len(nums))):
			if nums[j]+mn <= target:
				res += 2**(j-i)
				break
	return res
```

### sorting + binary search

Instead of doing two pointers, we can binary search for the right bound to take advantage of the sorted nature of the list.

```python
# O(nlogn)
def numSubseq(self, nums: List[int], target: int) -> int:
	MOD = 10**9+7
	res = 0
	nums.sort()
	  
	for i in range(len(nums)):
		mn = nums[i]
		# break early
		if mn*2 > target: break
	  
		# binary search for right bound, max_idx
		max_idx = i
		l, r = i, len(nums)-1
		while l <= r:
			m = (l+r)//2
	  
			if (
				nums[m]+mn <= target and
				(m == len(nums)-1 or nums[m+1]+mn > target)
			):
				max_idx = m
				break
			elif nums[m]+mn <= target:
				l = m+1
			else:
				r = m-1
		res += 2**(max_idx-i)
	return res % MOD
```

### sorting + two pointers

Instead of recomputing the binary search for each range, we can actually just move two pointers inwards greedily. If two values `mn` and `mx` satisfy the condition, then we can calculate it and then increase our `mn` (because we’ve just calculated all subsets using `mn` as minimum). Otherwise, decrease our `mx`.

```python
# O(nlogn)
def numSubseq(self, nums: List[int], target: int) -> int:
	MOD = 10**9+7
	res = 0
	nums.sort()
	  
	l, r = 0, len(nums)-1
	  
	while l <= r:
		mn, mx = nums[l], nums[r]
	  
		if mn+mx <= target:
			res += 2**(r-l)
			l += 1
		else:
			r -= 1
	return res % MOD
```
