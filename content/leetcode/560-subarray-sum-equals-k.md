---
type: leetcode
title: 560. subarray sum equals k
date: 2022-12-25
updated: 2024-08-28
tags:
  - prefix-sums
  - hashmap
---

Given an array of integers `nums` and an integer `k`, return _the total number of subarrays whose sum equals to_ `k`.

A subarray is a contiguous **non-empty** sequence of elements within an array.

## solution

We use the idea of prefix sum to more efficiently compute the sums of subarrays.

Initially, I thought to iterate through the prefix sums, and for each, to look back and see if any shorter prefixes could be subtracted to reach target $k$. However, this would be $O(n^2)$.

I then thought to optimize by using a hashmap to store the indices that had prefixes of certain values, then, when we iterate through the prefix array, we can check to see how many of the indices are before our current index. This would require some sort of $O(n)$ or $O(\log n)$ operation, to find which indices were valid.

Instead of looking backwards for valid subarrays ending at $i$, I decided instead to look forwards for valid subarrays starting at $i$. This way, I can use my hashmap, and just remove the counts from the hashmap as I move past them.

```python
def subarraySum(self, nums: List[int], k: int) -> int:
	prefix_sums = [0]
	for num in nums:
		prefix_sums.append(prefix_sums[-1] + num)

	sum_frequencies = Counter(prefix_sums)
	  
	ans = 0
	for s in prefix_sums:
		# moving past nums[s], need to decrement
		# that frequency from hashmap, because
		# we only look right for relevant values
		  
		# we remove before checking because we can't
		# form an empty subarray with ourselves
		sum_frequencies[s] -= 1
		ans += sum_frequencies[k+s]
	return ans
```

Note that it’s still possible (and slightly more efficient) to look backwards, as we can construct the prefix sums/hashmap as we go, as well as not have to worry about removing values from the hashmap.

```python
	def subarraySum(self, nums: List[int], k: int) -> int:
		ans = 0
		# count the number of times each prefix sum appears
		d = collections.defaultdict(int)
		d[0] = 1
		tally = 0
		for i, num in enumerate(nums):
			tally += num
			ans += d[tally-k]
			d[tally] += 1
		return ans
```
