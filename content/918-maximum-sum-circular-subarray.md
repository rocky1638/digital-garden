---
type: leetcode
title: 918. maximum sum circular subarray
tags:
  - prefix-sums
  - dp
  - kadane
aliases: 
parents:
  - "[[53-maximum-subarray]]"
children: 
supports: 
enemies: 
date: 2024-09-24
updated: 2024-09-24
---

Given a **circular integer array** `nums` of length `n`, return _the maximum possible sum of a non-empty **subarray** of_ `nums`.

A **circular array** means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.

A **subarray** may only include each element of the fixed buffer `nums` at most once. Formally, for a subarray `nums[i], nums[i + 1], ..., nums[j]`, there does not exist `i <= k1`, `k2 <= j` with `k1 % n == k2 % n`.

## solutions

### prefix + suffix sums

There’s two distinct cases: when we use the circular property of the array, and when we don’t.

When we don’t, it’s just [[53-maximum-subarray]], and so we can use Kadane’s algorithm.

However, when we do use the circular subarray property, we’re essentially tying together a suffix and a prefix of the array (such that they don’t overlap).

To efficiently find the best way to construct a subarray this way, we can create an array `max_suffix_to_right`, where `max_suffix_to_right[i]` contains the biggest suffix sum ending at `nums[-1]` that starts at `nums[i]` or later.

This way, for each prefix sum `nums[:i]`, we can simply add that prefix sum to the value at `max_suffix_to_right[i]`.

```python
# O(n)
def maxSubarraySumCircular(self, nums: List[int]) -> int:
	# Kadane's, for normal max subarray
	bestendinghere = -inf
	bestsofar = -inf
	for num in nums:
		bestendinghere = max(num, bestendinghere+num)
		bestsofar = max(bestendinghere, bestsofar)
	  
	# handle circular array
	max_suffix_to_right = []
	suffix = 0
	bestsuffixsofar = -inf
	for num in reversed(nums):
		suffix += num
		bestsuffixsofar = max(suffix, bestsuffixsofar)
		max_suffix_to_right.append(bestsuffixsofar)
	max_suffix_to_right = max_suffix_to_right[::-1]
	  
	best_circular = -inf
	prefix = 0
	for i, num in enumerate(nums[:-1]):
		prefix += num
		best_circular = max(
			best_circular,
			prefix+max_suffix_to_right[i+1]
		)
	  
	return max(best_circular, bestsofar)
```

### tricky kadane

A key observation is that in the second case above, we wanted a suffix + prefix to make a “circular subarray”. However, this can be thought of, inversely, as just removing a subarray from the middle of `nums` and taking the rest.

So, to maximize the circular subarray after removal, we want to remove the _minimum subarray_ from the middle. This can be done in the same pass with Kadane’s algorithm!

Be sure to catch the edge case of the minimum subarray being the entire array. This would imply an empty circular subarray, which is not allowed.

```python
def maxSubarraySumCircular(self, nums: List[int]) -> int:
	maxendinghere, minendinghere = 0, 0
	maxsofar, minsofar = nums[0], nums[0]
	totalsum = 0
	  
	for num in nums:
		# normal kadane's
		maxendinghere = max(maxendinghere+num, num)
		maxsofar = max(maxsofar, maxendinghere)
		  
		# kadane's (but minimum)
		minendinghere = min(minendinghere+num, num)
		minsofar = min(minsofar, minendinghere)
		  
		totalsum += num

	if totalsum == minsofar:
		return maxsofar
	return max(maxsofar, totalsum-minsofar)
```
