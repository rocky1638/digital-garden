---
type: leetcode
title: 689. maximum sum of 3 non-overlapping subarrays
tags:
  - recursion
  - memoization
  - dp
  - prefix-sums
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-03
updated: 2024-10-03
---

Given an integer array `nums` and an integer `k`, find three non-overlapping subarrays of length `k` with maximum sum and return them.

Return the result as a list of indices representing the starting position of each interval (**0-indexed**). If there are multiple answers, return the lexicographically smallest one.

## solutions

### top-down recursion w/ memoization

Immediately, the intuition should be that we can just simply try to use DFS to explore the possibility space, choosing to start a subarray at an index, or skip the index.

```python
# O(k*2^n) - 2 branches n times, O(k) sum operation per node in DFS
# With memoization, there are O(3n) ~ O(n) unique states, so O(nk)
def maxSumOfThreeSubarrays(self, nums: List[int], k: int) -> List[int]:
	memo = {}
	def recurse(idx, completed):
		if completed == 3:
			return 0, []
		  
		# break early if not enough values
		# for remaining subarrays
		remaining_vals = len(nums)-idx
		if (3-completed)*k > remaining_vals:
			return 0, []

		if (idx, completed) in memo:
			return memo[(idx, completed)][0], memo[(idx, completed)][1]
		  
		# start next subarray at current index
		# take k values
		subsum = sum(nums[idx:idx+k])
		rest_sum, rest_indices = recurse(idx+k, completed+1)
		  
		# skip this index
		skip_sum, skip_indices = recurse(idx+1, completed)
		  
		total, indices = None, None

		# >= because prefer take over skip
		# (gives lexicographically lower answer)
		if subsum+rest_sum >= skip_sum:
			total, indices = subsum+rest_sum, [idx]+rest_indices
		else:
			total, indices = skip_sum, skip_indices

		memo[(idx, completed)] = [total, indices]
		return total, indices

	_, start_indices = recurse(0, 0)
	return start_indices
```

We can then add prefix sums to remove the $O(k)$ operation in the recursive step, improving our runtime to $O(n)$.

```python
def maxSumOfThreeSubarrays(self, nums: List[int], k: int) -> List[int]:
	prefix_sums = [0]
	for num in nums:
		prefix_sums.append(prefix_sums[-1]+num)

	memo = {}
	def recurse(idx, completed):
		if completed == 3:
			return 0, []
	  
		# break early if not enough values
		# for remaining subarrays
		remaining_vals = len(nums)-idx
		if (3-completed)*k > remaining_vals:
			return 0, []

		if (idx, completed) in memo:
			return memo[(idx, completed)][0], memo[(idx, completed)][1]
		  
		# start next subarray at current index
		# take k values
		subsum = prefix_sums[idx+k]-prefix_sums[idx]
		rest_sum, rest_indices = recurse(idx+k, completed+1)
		  
		# skip this index
		skip_sum, skip_indices = recurse(idx+1, completed)
		  
		total, indices = None, None
		# >= because prefer take over skip
		# (gives lexicographically lower answer)
		if subsum+rest_sum >= skip_sum:
			total, indices = subsum+rest_sum, [idx]+rest_indices
		else:
			total, indices = skip_sum, skip_indices

		memo[(idx, completed)] = [total, indices]
		return total, indices

	_, start_indices = recurse(0, 0)
	return start_indices
```
