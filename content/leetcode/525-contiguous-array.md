---
type: leetcode
title: 525. contiguous array
date: 2022-12-20
updated: 2024-09-01
tags:
  - prefix-sums
  - hashmap
---

Given a binary array `nums`, return _the maximum length of a contiguous subarray with an equal number of_ `0` _and_ `1`.

## solution

I originally thought to use prefix sum pattern, but it timed out likely due to the $O(n)$ iteration through the prefix array for each value in the array.

The solution is kind of like an extension of prefix sums, but with a twist.

It is best to think about this problem like a path where each 1 makes you go uphill, and each 0 makes you go downhill. We start at elevation of 0, and if we ever reach elevation 0 again, we know that we’ve traversed a balanced section. Also, the first time we reach a new elevation, we should store where it is. The next time we reach this **same** elevation, we know that portion we’ve walked is balanced!

For a similar conceptual problem, see [[523-continuous-subarray-sum]].

```python
def findMaxLength(self, nums: List[int]) -> int:
	balance_to_leftmost_idx: {0: -1}
	  
	ans = 0
	balance = 0
	for i, num in enumerate(nums):
		if num == 1:
			balance += 1
		else:
			balance -= 1
		if balance in balance_to_leftmost_idx:
			ans = max(ans, i-balance_to_leftmost_idx[balance])
		else:
			balance_to_leftmost_idx[balance] = i
	return ans
```
