---
type: leetcode
title: 939. minimum area rectangle
tags:
  - geometry
  - sorting
aliases: 
parents: 
children: 
supports:
  - "[[2013-detect-squares]]"
enemies: 
date: 2022-12-30
updated: 2024-05-19
---

You are given an array of points in the **X-Y** plane `points` where `points[i] = [xi, yi]`.

Return _the minimum area of a rectangle formed from these points, with sides parallel to the X and Y axes_. If there is not any such rectangle, return `0`.

## solution

On first thought, it’s easy to think about trying to construct every possible group of four points, but this achieves a runtime of $O(n^4)$.

Instead, the key insight here is that, similar to many other “square from points” problems like [[2013-detect-squares]], we only need two points to unique identify a rectangle!

In the solution below, we enumerate every possible pair of points. If we have two diagonal points $(x_1, y_1)$ and $(x_2, y_2)$ such that:
1. $x_1 \neq x_2$ and $y_1 \neq y_2$ (the two points are indeed diagonal, not on the same plane).
2. $(x_1, y_2)$ and $(x_2, y_1)$ exist in our set of points (the inverse diagonal).

Then we know that we can create a rectangle with those four points! Because this enumeration step is $O(n^2)$, we can sort our enumerated pairs by the area of the rectangle they would form without increasing asymptotic runtime. This allows us to return on the first valid rectangle we find.

```python
def minAreaRect(self, points: List[List[int]]) -> int:
	# for O(1) existence check
	ps = set([(x,y) for x, y in points])
	  
	# (p1, p2, area)
	pairs = []
	for i in range(len(points[:-1])):
		for j in range(i+1, len(points)):
			p1, p2 = points[i], points[j]
			x1, y1 = p1
			x2, y2 = p2
			distance = abs(x1-x2) * abs(y1-y2)
			pairs.append([p1, p2, distance])

	pairs.sort(key=lambda x: x[2])
	  
	for p1, p2, distance in pairs:
		x1, y1 = p1
		x2, y2 = p2
	  
	if x1 != x2 and y1 != y2:
		if (x1, y2) in ps and (x2, y1) in ps:
			return abs(x1-x2) * abs(y1-y2)

	return 0
```
