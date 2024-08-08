---
type: leetcode
title: 1762. buildings with an ocean view
tags:
  - monotonic-stack
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-11
updated: 2024-07-11
---

There are `n` buildings in a line. You are given an integer array `heights` of size `n` that represents the heights of the buildings in the line.

The ocean is to the right of the buildings. A building has an ocean view if the building can see the ocean without obstructions. Formally, a building has an ocean view if all the buildings to its right have a **smaller** height.

Return a list of indices **(0-indexed)** of buildings that have an ocean view, sorted in increasing order.

## solution

Use a monotonic stack to find all the buildings that don’t have a taller building to the right.

```python
def findBuildings(self, heights: List[int]) -> List[int]:
	stack = []
	  
	for i, h in enumerate(heights):
		while stack and stack[-1][0] <= h:
			stack.pop()
		stack.append((h, i))
	return [x[1] for x in stack]
```
