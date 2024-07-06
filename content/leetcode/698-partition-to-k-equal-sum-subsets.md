---
type: <% tp.file.cursor() %>
title: <% tp.file.cursor() %>
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-06-12
---

Given an integer array `nums` and an integer `k`, return `true` if it is possible to divide this array into `k` non-empty subsets whose sums are all equal.

## solutions

### backtracking w/ early exit

We can recursively build up a solution with backtracking using $k$ subsets, each set initially to 0. We then just try adding values to the first available subset that will not exceed our target value.

The main optimization that we make here is first sorting the `nums` array descending. Then, we have an early exit on line 22. This condition works, because if the value at `subsets[i]` is equal to zero, we don’we don't actually have to check any of the other subsets, because we know that the values remaining are not able to reach target for any new subset.

Without the early exit, this has runtime $O(k^n)$, but is much faster with the early exit.

```python
def canPartitionKSubsets(self, nums: List[int], k: int) -> bool:
	s = sum(nums)

	if s % k != 0:
		return False
	  
	target = s // k
	subsets = [0]*k
	nums.sort(reverse=True)
	  
	def backtrack(idx):
		if idx == len(nums):
			return True
		  
		ans = False
		for i, subset in enumerate(subsets):
			if nums[idx] + subset <= target:
				subsets[i] += nums[idx]
				ans = ans or backtrack(idx+1)
				subsets[i] -= nums[idx]
		  
			if subsets[i] == 0:
				break
		  
		return ans
	  
	return backtrack(0)
```

### nested backtracking

Instead of building all the subsets at the same time, we can build one subset at a time, giving us runtime $O(k2^n)$.

Note that this solution still does guarantee that a solution will be found if it exists, because we will backtrack on all possible ways to build the first subset, not just the first way we find.

```python
def canPartitionKSubsets(self, nums, k):
	if sum(nums) % k != 0:
		return False
	  
	nums.sort(reverse = True)
	target = sum(nums) / k
	visited= set()
	  
	def backtrack(idx, count, currSum):
		if count == k:
			return True

		# try to build next subset
		if target == currSum:
			return backtrack(0, count + 1, 0)
		  
		for i in range(idx, len(nums)):
			# skip duplicates if last same number was skipped
			if i > 0 and (i - 1) not in visited and nums[i] == nums[i - 1]:
				continue
		  
			if i in visited or currSum + nums[i] > target:
				continue
		  
			visited.add(i)
				  
			if backtrack(i + 1, count, currSum + nums[i]):
				return True

			visited.remove(i)
		  
		return False
	
	return backtrack(0, 0, 0)
```

### dp with bitmasks

Also has runtime on the order of $O(2^n)$.
