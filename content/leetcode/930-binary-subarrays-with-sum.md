---
type: leetcode
title: 930. binary subarrays with sum
tags:
  - hashmap
  - prefix-sums
  - two-pointer
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-03
updated: 2024-10-03
---

Given a binary array `nums` and an integer `goal`, return _the number of non-empty **subarrays** with a sum_ `goal`.

A **subarray** is a contiguous part of the array.

## solutions

### hashmap of prefix sum frequencies

Very similar to other problems like [[523-continuous-subarray-sum]] and [[560-subarray-sum-equals-k]].

We can use a hashmap to store frequencies of our prefix sums, and lookback as we traverse to accumulate our total answer of subarrays.

```java
// O(n), O(n) space
class Solution {  
	public int numSubarraysWithSum(int[] nums, int goal) {  
		HashMap<Integer, Integer> prefixes = new HashMap<>();  
		prefixes.put(0, 1);  
		
		int res = 0;  
		int prefix = 0;  
		
		for (int val : nums) {  
			prefix += val;  
		
			if (prefixes.containsKey(prefix-goal)) {  
				res += prefixes.get(prefix-goal);  
			}  
			prefixes.put(prefix, prefixes.getOrDefault(prefix, 0)+1);  
		}  
		
		return res;  
	}  
}
```

### two pointers

We normally could two pointer this pretty easily, but it’s more tricky as zeroes mean that we could expand/contract our window while keeping the same window sum.

The key realization is that if we have some subarray `[0,0,1,1]`, the number of subarrays that sum to 2 is equal to one plus the number of prefix zeroes. In this case, we have `[0,0,1,1]`, `[0,1,1]`, and `[1,1]`.

So, we can use a modified sliding window approach, where we move our left window pointer up while `window_sum > goal` (the normal condition), as well as when `nums[l] == 0`. While we do this, we can keep track of how many unbroken prefix zeroes exist before our window. If we see a `1`, we reset this number.

Then, after we’ve shrunk our window, if `window_sum == goal`, we use the prior logic and add `1+prefix_zeros` to our answer.

```python
class Solution:  
	def numSubarraysWithSum(self, nums: List[int], goal: int) -> int:  
	l = 0  
	window_sum = 0  
	prefix_zeros = 0  
	res = 0  
	
	# [1,0,0,1,1]  
	# [1,0,0,1] -> prefix_zeroes = 0, res += 1  
	# [1,0,0,1,1] -> now shrink  
	# shrink: [0,0,1,1] -> prefix_zeroes = 0  
	# shrink: [0,1,1] -> prefix_zeroes = 1  
	# shrink: [1,1] -> prefix_zeroes = 2 (done shrinking)  
	# res += 1 + 2  
	for r in range(len(nums)):  
		window_sum += nums[r]  
	
		while l < r and (nums[l] == 0 or window_sum > goal):  
			if nums[l] == 1:  
				prefix_zeros = 0  
			else:  
				prefix_zeros += 1  
	
			window_sum -= nums[l]  
			l += 1  
	
		if window_sum == goal:  
			res += 1 + prefix_zeros  
	
	return res
```
