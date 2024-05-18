---
created_at: 2022-12-09
type: leetcode
title: 739. daily temperatures
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/daily-temperatures/
date: 2022-12-09
updated: 2024-04-28
tags:
  - monotonic-stack
---

Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ `ith` _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

## solution

We iterate through the array, and append the temperatures, as well as the index of the temperature to our stack. Then, for each value in the stack, we see if the current value is larger.

If the current value is larger, that means that the current value is the first value after that stack value that is larger than it. We record the index difference, and pop this stack value off of the stack because it’s now been accounted for.

```python
def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
	n = len(temperatures)
	ans = [0]*n
	
	stack = []
	
	for idx, temp in enumerate(temperatures):
		while stack and stack[-1][0] < temp:
			prev_temp, prev_idx = stack.pop()
			ans[prev_idx] = idx-prev_idx
		stack.append((temp, idx))
	return ans
```
