---
type: leetcode
title: "2439. minimize array value"
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-03-30
---

You are given a **0-indexed** array `nums` comprising of `n` non-negative integers.

In one operation, you must:

- Choose an integer `i` such that `1 <= i < n` and `nums[i] > 0`.
- Decrease `nums[i]` by 1.
- Increase `nums[i - 1]` by 1.

Return _the **minimum** possible value of the **maximum** integer of_ `nums` _after performing **any** number of operations_.

## solutions

First of all, it’s important to reframe this question as a a sort of “transferring of value” from the right towards the left.

Notice that when we decrease `nums[i]` by 1, we “give” it to `nums[i-1]`. Transitively, this single unit can then continue travelling leftward as far as the beginning of the array. Logically, this means that any value at $i$ can transfer value to any other index $<i$.

Conversely, this means that we can _never_ transfer any units rightwards.

In this view, our end goal is to “distribute” the wealth as evenly as possible, with the constraint that we can only transfer things leftwards.

### iterative scan with prefix sum array

From the above intuition, we can derive some insights from base cases:

1. The optimally distributed maximum height in an array of length 1 will be equal to the height of the single bar.
2. For two bars, if the bar at $i=1$ is taller than the bar at $i=0$, then the best maximum height is the ceiling of the average of the two bars.

![[2439-minimize-array-value-1.png]]

3. However, if the left bar is taller, then the optimal maximum is simply the height of the left bar, because we can’t transfer anything rightwards.
	- This leads to the intuition that as we scan rightwards through the bars and keep track of an optimal height, we can _never_ improve on it, because even if we see a shorter bar later on, this bar can’t take the load off of any prior bars.

![[2439-minimize-array-value-2.png]]

4. Given any number of monotonically increasing bars, the optimal distribution will lead to a maximum bar height of `math.ceil(average(sum(bars)))`.

![[2439-minimize-array-value-3.png]]

Given this intuition, we realize that we can scan through the array from left to right, computing the average of all the bars from $0$ to $i$, and comparing that to our previous best.

Our running best can only get worse, hence the line `ans = max(ans, math.ceil(average))`.

```python
def minimizeArrayValue(self, nums: List[int]) -> int:
	prefix_sum = [nums[0]]
	ans = nums[0]

	for num in nums[1:]:
		prefix_sum.append(prefix_sum[-1] + num)
		ans = max(ans, math.ceil(prefix_sum[-1] / len(prefix_sum)))
	return ans

```
