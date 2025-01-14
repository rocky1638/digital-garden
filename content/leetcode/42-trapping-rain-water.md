---
title: 42. trapping rainwater
type: leetcode
aliases: 
difficulty: 🔴
link: https://leetcode.com/problems/trapping-rain-water/
date: 2022-11-24
updated: 2024-10-28
tags:
  - two-pointer
  - array
---

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

## solutions

### two iterations

The brute force way to approach this is to iterate through the heights, and for each height, we go outwards with two pointers towards the edges of the structure to find the tallest enclosing walls on each side.

We can improve on this by memoizing the tallest wall to the left and right of each index. Furthermore, we only really need to store one of them, because the other direction can be stored in a single value as we iterate.

```python
def trap(self, height: List[int]) -> int:
	maxtoleft = 0
	maxtoright = [0]
	ans = 0
	
	# create maxtoright array
	for h in reversed(height[1:]):
		maxtoright.append(max(h, maxtoright[-1]))
		maxtoright = maxtoright[::-1]
	
	# iterate from left
	for i in range(len(height)):
		minwall = min(maxtoleft, maxtoright[i])
		if height[i] < minwall:
			ans += minwall - height[i]
		maxtoleft = max(maxtoleft, height[i])
	return ans
```

### one iteration

We can actually improve further to only one iteration by using [[two-pointers]] going inwards from the edges, and keep track of both max from left and max from right in two single values.

The key insight is that the amount of water stored at index `i` is only dependent on the smaller of the two maximum walls!

For example, if we are at an index where we know that the left maximum wall is shorter than the right maximum wall so far, we can safely use the height of left maximum wall to calculate the amount of water stored, and *don’t actually care about the rest of the walls to the right that we haven’t checked yet.*

This is because in both cases, our answer stays the same:

- If there’s a wall to the right that we haven’t seen yet that is taller than `rightmax`, it doesn’t matter because our water stored is still dependent on the current `leftmax`.
- If there’s a wall to the right that we haven’t seen yet that is shorter than `rightmax`, it’s irrelevant because `rightmax` is already bigger.

```python
def trap(self, height: List[int]) -> int:
	n = len(height)
	ans = 0
	  
	l, r = 0, n-1
	lmax = rmax = 0
	  
	while l < r:
		# set lmax and rmax of edge heights
		# to start
		lmax = max(lmax, height[l])
		rmax = max(rmax, height[r])
	  
		# if lmax is smaller, we don't care if there's
		# a bigger wall to the right bigger than rmax...
		# we're already limited by lmax
		# so, we can calculate the water trapped for l+1
		if lmax < rmax:
			l += 1
			ans += max(0, lmax - height[l])
		# vice versa for right
		else:
			r -= 1
			ans += max(0, rmax - height[r])
	  
	return ans
```

Just another option if one of them happens to make more sense to me at any given time…

```python
def trap(self, height: List[int]) -> int:
	n = len(height)
	ans = 0
	  
	l, r = 0, n-1
	lmax, rmax = height[l], height[r]
	  
	while l < r:
		if lmax < rmax:
			l += 1
			lmax = max(lmax, height[l])
			ans += max(0, lmax - height[l])
		else:
			r -= 1
			rmax = max(rmax, height[r])
			ans += max(0, rmax - height[r])
	  
	return ans
```

### monotonic stack

We can also use a [[monotonic-stack]] here to solve this problem.

If we maintain an increasing monotonic stack as we go from left to right, we can calculate the trapped water for any wall $m$ in the stack once we reach a taller wall $r$ (because $r$ will stop the water that’s trapped on the level of $m$). Furthermore, we can see that the left wall will be whatever value is below $m$ in the stack, because that’s the closest wall to the left that’s taller than $m$.

```python
def trap(self, height: List[int]) -> int:
	stack = []
	ans = 0
	  
	for r, h in enumerate(height):
		while stack and height[stack[-1]] < h:
			base_idx = stack[-1]
			stack.pop()
			if not stack: break
			l_idx = stack[-1]
			water_height = min(h, height[l_idx]) - height[base_idx]
			width = r - l_idx - 1
			ans += width * water_height
		stack.append(r)
	return ans
```

## references

- https://leetcode.com/problems/trapping-rain-water/solutions/5010020/monotonic-stack-vs-priority-queue-using-pyplot-explain-3ms-beats-99-10
