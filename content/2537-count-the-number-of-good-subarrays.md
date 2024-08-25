---
type: leetcode
title: 2537. count the number of good subarrays
tags:
  - sliding-window
  - two-pointer
  - math
aliases: 
parents: 
children:
  - "[[2444-count-subarrays-with-fixed-bounds]]"
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-17
---

Given an integer array `nums` and an integer `k`, return _the number of **good** subarrays of_ `nums`.

A subarray `arr` is **good** if it there are **at least** `k` pairs of indices `(i, j)` such that `i < j` and `arr[i] == arr[j]`.

A **subarray** is a contiguous **non-empty** sequence of elements within an array.

## solution

The first thing to figure out here is just the question. We realize that if a subarray has $n$ copies of some value $x$, then there will be $n \choose x$ pairs that contribute towards `k`. A simpler way to calculate this is to realize that if we have $n$ copies of a value and then adding another copy, we will add a total of $n$ more pairs to that set of $x$.

With that figured out, it makes sense to use a sliding window, as we’re looking for subarrays that meet some sort of invariant.

We can slide `r` to the right until the subarray is “good”. The first realization is that if `nums[l:r+1]` is good, then every subarray to `nums[l:]` is also good.

So, we’ve found every subarray starting at index `l` that is good! Just like a problem like [[2444-count-subarrays-with-fixed-bounds]], we use the idea of finding all subarrays anchored at some point to accurately enumerate subarrays. This means we now want to find all “good” subarrays that start at index `l+1`, and etc.

So we can increment `l` until the subarray `nums[l:r+1]` is invalid, but for each increment where it’s still valid, we can add all of those subarrays as well to our final count.


> [!attention]
> In the solution below, I didn't realize that there was a more elegant way to count subarrays when sliding `l` to the right (like I described above), and so I used a more traditional sliding window template, opting to not slide `r` up if we had previously just moved `l`.

```python
def countGood(self, nums: List[int], k: int) -> int:
	n = len(nums)
	freq = Counter()
	  
	ans = 0
	count = 0
	l = r = 0
	incremented_l = False
	while r < n:
		if not incremented_l:
			# add to window
			freq[nums[r]] += 1
		  
			# update num pairs
			if freq[nums[r]] > 1:
				count += freq[nums[r]]-1

		# subarray is now good
		# all subarrays extended right are also valid
		if count >= k:
			ans += n-r
			# we've now accounted for all good
			# subarrays starting at l, so advance l
			freq[nums[l]] -= 1
			count -= freq[nums[l]]
			# don't advance r in this case, as [l+1:r]
			# could be a good subarray
			l += 1
			incremented_l = True
		else:
			r += 1
			incremented_l = False
	return ans
```
