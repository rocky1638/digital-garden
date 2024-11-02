---
type: leetcode
title: 1838. frequency of the most frequent element
tags:
  - sorting
  - greedy
  - sliding-window
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-10-30
---

The **frequency** of an element is the number of times it occurs in an array.

You are given an integer array `nums` and an integer `k`. In one operation, you can choose an index of `nums` and increment the element at that index by `1`.

Return _the **maximum possible frequency** of an element after performing **at most**_ `k` _operations_.

## solutions

### brute force

We first do the brute force solution to get an intuition of the problem. For every possible `target`, we compute how many smaller values we can convert into `target` given `k` operations. Note that we can greedily convert the values that are closest in value to `target` first.

```python
# O(n^2)
def maxFrequency(self, nums: List[int], k: int) -> int:
	# O(n)
	c = Counter(nums)
	# O(nlogn)
	freqs_sorted = sorted([(val, freq) for val, freq in c.items()])

	def calculate(target, start_idx):
		count = 0
		k_rem = k
		i = start_idx-1
	  
		while i >= 0 and k_rem > 0:
			# smaller number that we want to add to to reach target
			smaller_num, smaller_freq = freqs_sorted[i]
	  
			diff = target-smaller_num
	  
			# if we can't make it reach with remaining k, we're done
			if k_rem < diff: break
	  
			# either increment all of the number, or the maximum we can
			num_changed = min(smaller_freq, k_rem//diff)
	  
			k_rem -= diff * num_changed
			count += num_changed
			i -= 1
		return count

	res = 0
	for i, (num, freq) in enumerate(freqs_sorted):
		res = max(res, freq+calculate(num, i))
	return res
```

### sorting + sliding window

The realization is that in the brute force solution, we have a significant amount of recalculation when we choose each target, as we look back on the same overlapping values again and again. This gives us the intuition that perhaps sliding window can work here.

With a sliding window, we can expand our window to the right as long as we have enough operations to even out stuff in our window, and slide our window up on the left when we run out of operations.

Note that we don’t want to create a frequency map/list like I did in the previous solution as that would make a sliding window approach more convoluted and difficult.

```python
def maxFrequency(self, nums: List[int], k: int) -> int:
	"""
	example:
	1,1,2,4, k = 5
	-> [1,1],2,4 (k_used = 0, count=2)
	-> [1,1,2],4 (k_used = 2, count=3) (our window is essentially [2,2,2],4)
	-> [1,1,2,4] (k_used = 8, count=4) (window is [4,4,4,4]) -- we went over so shorten window
	-> 1,[1,2,4] (k_used = 5, count=3)
	"""
	nums.sort()
	  
	res = 1
	l = 0
	rem_k = k
	for r in range(1, len(nums)):
		# add nums[r] to the window
		# rem_k will decrease by (nums[r]-nums[r-1]) * window_len
		diff = nums[r]-nums[r-1]
		rem_k -= diff*(r-l)
	  
		while rem_k < 0:
			removed = nums[l]
			rem_k += nums[r]-nums[l]
			l += 1
		res = max(res, r-l+1)
	
	return res
```
