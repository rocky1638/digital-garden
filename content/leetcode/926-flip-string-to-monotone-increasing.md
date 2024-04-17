---
type: leetcode
title: 926. flip string to monotone increasing
tags:
  - dp
  - prefix-sums
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-04-04
---

A binary string is monotone increasing if it consists of some number of `0`'s (possibly none), followed by some number of `1`'s (also possibly none).

You are given a binary string `s`. You can flip `s[i]` changing it from `0` to `1` or from `1` to `0`.

Return _the minimum number of flips to make_ `s` _monotone increasing_.

## solutions

### prefix sum array

The intuition here is that for a monotonically non-decreasing string of 0s and 1s, we must have a string of all 0s, all 1s, or a block of 0s followed by a block of 1s.

As such, that means we need to have some index $i$ where our string switches from 0s to 1s. We can check every index in code. The number of flips we need for any given index $i$ is the number of 1s to the left of $i$ (which need to become 0s), and the number of zeroes to the right of $i$ (which need to become ones).

To make the checks $O(1)$, we use a prefix sum array.


> [!hint]
> Instead of prefix sums, we could also keep two dynamic programming arrays: one storing the number of 1->0 flips going from the left, and one storing the number of 0->1 flips going from the right.
>
> Then, we could just return the smallest sum of these two values at any index.
>
> This follows the same underlying logic of trying to find the best index $i$ to switch from 0s to 1s.

```python
def minFlipsMonoIncr(self, s: str) -> int:
# initialize with empty prefix
prefix_sums = [0]
  
for c in s:
	if c == "0":
		prefix_sums.append(prefix_sums[-1])
	else:
		prefix_sums.append(prefix_sums[-1]+1)
  
	ans = float("inf")
	for i in range(len(s)):
		ones_to_left = prefix_sums[i]
  
		# number of chars remaining to the right
		spaces_to_right = len(s) - i - 1
		# what the sum would be if all the remaining
		# spaces to the right were ones
		if_all_ones = prefix_sums[i+1] + spaces_to_right
		# we use if_all_ones to deduce how many zeroes exist
		zeroes_to_right = if_all_ones - prefix_sums[-1]
		# flips required is the ones to left and zeroes to right
		ans = min(ans, ones_to_left + zeroes_to_right)

return ans
```
