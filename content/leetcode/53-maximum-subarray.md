---
title: 53. maximum subarray
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/maximum-subarray/
date: 2022-11-15
updated: 2024-09-02
tags:
  - dp
  - array
---

## solutions

### kadane’s algorithm

```python
class Solution:
	def maxSubArray(self, nums: List[int]) -> int:
		best, bestendinghere = float("-inf"), float("-inf")
		for num in nums:
			bestendinghere = max(bestendinghere + num, num)
			best = max(best, bestendinghere)
		return best
```

- this question is essentially dynamic programming.
- at each index of the array, we ask ourselves what the maximum subarray is that has its right bound at the current index.
	- we can either add on to the maximum subarray that ended at the previous index, or start a new subarray.
	- `maxendinghere = max(n, maxendinghere+n)`

essentially, if $A_i$ is equal to the value of the array at index $i$ and $M_i$ is equal to the maximum subarray ending at index $i$, then our optimization function is

$$
M_i=
\begin{cases}
A_i \text{ if } i=0 \\
\max(A_i, M_{i-1}+A_i) \text{ otherwise}
\end{cases}
$$

### prefix sums with constant space

Similar class of problems to: [[523-continuous-subarray-sum]], [[525-contiguous-array]].

```python
class Solution:

def maxSubArray(self, nums: List[int]) -> int:

res = -inf

prefix = 0

minprefixsofar = 0

  

for num in nums:

prefix += num

res = max(res, prefix-minprefixsofar)

minprefixsofar = min(minprefixsofar, prefix)

return res
```
