---
type: leetcode
title: 128. longest consecutive sequence
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/longest-consecutive-sequence/
date: 2022-12-13
updated: 2024-08-31
tags:
  - union-find
  - hashmap
---

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

## solutions

### hashmap trick

The brute force method is for each number, to continually see if the next number appears in the array.

The key “trick” or intuition that helps for this problem is realizing that a number will be the start of a sequence if `num-1` does not exist in the set. We can check for this in constant time if we use a set.

Then, for each number, if it is the smallest number in a sequence, we iterate as long as the next number is also in the set.

```python
def longestConsecutive(self, nums: List[int]) -> int:
	if not nums:
		return 0

	ans = 1
	s = set(nums)

	for num in nums:
		# if the lower number is in nums, we wanna start with that one
		if num-1 not in s:
			cur = num
			count = 1
			while cur+1 in s:
				cur += 1
				count += 1 
				ans = max(ans, count)
	return ans
```

### union find

I have come from the future, now with a more solid understanding of union find, and this problem definitely seems like union find the more you think about it.

Reframe the situation as “each node $n$ has edges to $n-1$ and $n+1$. Find the size of the largest component”.

```python
def longestConsecutive(self, nums: List[int]) -> int:
	if not nums:
		return 0
	  
	parents = {num: num for num in nums}
	sizes = {num: 1 for num in nums}
	
	def union(x, y):
		if x not in parents or y not in parents:
			return
		px, py = find(x), find(y)

		# already connected
		if px == py:
			return
	  
		# px is smaller
		if sizes[px] > sizes[py]:
			px, py = py, px
	  
		# py is new parent
		parents[px] = py
		sizes[py] += sizes[px]
	  
	def find(x):
		if x != parents[x]:
			parents[x] = find(parents[x])
		return parents[x]
	  
	for num in nums:
		union(num-1, num)
		union(num, num+1)
	  
	return max(sizes.values())
```
