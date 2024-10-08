---
type: leetcode
title: 995. minimum number of k consecutive flips
tags:
  - queue
  - sliding-window
  - greedy
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-09-14
---

You are given a binary array `nums` and an integer `k`.

A **k-bit flip** is choosing a **subarray** of length `k` from `nums` and simultaneously changing every `0` in the subarray to `1`, and every `1` in the subarray to `0`.

Return _the minimum number of **k-bit flips** required so that there is no_ `0` _in the array_. If it is not possible, return `-1`.

A **subarray** is a **contiguous** part of an array.

## solutions

### greedily flip while scanning

We iterate from left to right, and whenever we see a 0 at index $i$, we flip the array from `nums[i:i+k]`.

We can do this because we have no choice of the length of subarray we can flip (it needs be length `k`), and we know that we can’t possibly _not_ flip this index (because if we keep iterating, we’ll miss out on flipping this 0 and will not reach a valid answer).

```python
# O(nk) - we might call flip_k at every index
def minKBitFlips(self, nums: List[int], k: int) -> int:
	# O(k)
	def flip_k(idx):
		for i in range(idx, idx+k):
			nums[i] ^= 1
	  
	res = 0
	i = 0
	while i < len(nums):
		if nums[i] == 0:
			if i + k <= len(nums):
				flip_k(i)
				res += 1
			else:
				return -1
		else:
			i += 1
	return res
```

### sliding window w/ queue

Instead of manually flipping the actual values in the array, we instead just keep track of all the relevant flips that have occurred in the past, that affect our current value at index $i$.

Basically, we know that all of the flips in the range $(i-k, i)$ will affect the value at $i$, because the window has length $k$. We keep track of all the operations the we did (flip/no-flip) for the given window looking backwards, while also keeping track of the current flip state affecting $i$ (each flip in the past $k$ toggles this state).

Then, we can easily stop considering flips that are no longer relevant (falling out of the window) by popping off of the left of the queue as they fall out of the $k$-length window.

```python
# O(n)
def minKBitFlips(self, nums: List[int], k: int) -> int:
	flips = deque()
	flip_state = 0
	res = 0
	  
	for i, num in enumerate(nums):
		# check if a previous flip
		# is no longer relevant
		if i >= k:
			# flip_state: 0 1 0 1
			# prev_flip: 0 1 1 0
			# res: 0 0 1 1 -- XOR!
			flip_state ^= flips.popleft()

		# we need to flip (unflipped 0, or flipped 1)
		if num == flip_state:
			if i + k > len(nums):
				return -1
			flips.append(1)
			flip_state ^= 1 # toggle flip state
			res += 1
		else:
			flips.append(0)
	return res
```

### constant space

This is really clever and basically impossible to come up with an interview, but essentially we don’t even need to maintain a queue. We can instead just keep track of the number of flips in our window, as well as the indices where we performed a flip, by tracking it within `nums` by modifying `nums[i] = 2` if we end up flipping index $i$.

The logic for how the window works is similar, but instead of explicitly maintaining flip state, we just maintain the total number of flips conducted within the window, and check the parity of that value.

```python
def minKBitFlips(self, nums: List[int], k: int) -> int:
	flips = 0
	res = 0
	  
	for i, num in enumerate(nums):
		# remove a flip if falling edge was flipped
		if i >= k and nums[i-k] >= 2:
			flips -= 1
	  
		# we need to flip
		if (flips%2) == num:
			if i + k > len(nums):
				return -1
			nums[i] += 2
			flips += 1
			res += 1
	return res
```
