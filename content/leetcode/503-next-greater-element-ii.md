---
type: leetcode
title: 503. next greater element ii
tags:
  - monotonic-stack
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-20
---

Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return _the **next greater number** for every element in_ `nums`.

The **next greater number** of a number `x` is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.

## solution

Same as [[496-next-greater-element-i]], but we iterate through the array twice using modulo.

```python
def nextGreaterElements(self, nums: List[int]) -> List[int]:
stack = []
n = len(nums)
ans = [-1] * n
  
"""
[5,4,3,2,1] -> [5,4,3,2,1,5,4,3,2]
"""
  
for i in range(2*n-1):
while stack and stack[-1][0] < nums[i%n]:
_popped, idx = stack.pop()
ans[idx] = nums[i%n]
stack.append((nums[i%n], i%n))
  
return ans
```
