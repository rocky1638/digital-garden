---
type: leetcode
title: 149. max points on a line
tags:
  - hashmap
  - math
  - geometry
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-10
updated: 2024-10-10
---

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane, return _the maximum number of points that lie on the same straight line_.

## solutions

### y = mx+b

My initial thoughts were that any two points will lie on a line, but then we need to find all the other points that lie on the same line, or satisfy the same $y=mx+b$ equation.

So, I loop through every pair of points, and then for each created slope, look through every other point to see if it satisfies the line. This is $O(n^3)$.

```python
def maxPoints(self, points: List[List[int]]) -> int:
	"""
	brute force:
	- for each point, take another point and then try to find all other points
	on that line
	
	(1,1)
	(3,2)
	(5,3)
	
	1. solve for slope
	m = (2-1)/(3-1) = 1/2
	
	2. solve for intercept
	1 = 1/2(1) + b
	b = 1/2
	
	# test every other point to see if it
	# satisfies this equation
	y = 0.5x + 0.5
	
	there are n^2 pairs of points, each pair takes O(n) -> O(n^3)
	"""
	def calculate_slope(x1, y1, x2, y2):
		# (x1, y1) is more left
		if x1 > x2:
			x1, x2 = x2, x1
			y1, y2 = y2, y1
	
		return (y2-y1)/(x2-x1)
	
	def calculate_intercept(x, y, m):
		return y-m*x
	
	if len(points) < 3:
		return len(points)
	
	res = 0
	for i in range(len(points)):
		x1, y1 = points[i]
		for j in range(i+1, len(points)):
			x2, y2 = points[j]
	
			# vertical line
			if x1 == x2:
				m = inf
			else:
				m = calculate_slope(x1, y1, x2, y2)
				b = calculate_intercept(x1, y1, m)
	
			tally = 2
			for k in range(len(points)):
				if i == k or j == k: continue
				if m == inf:
					if points[k][0] == x1:
						tally += 1
				elif points[k][1] == m*points[k][0]+b:
					tally += 1
			res = max(res, tally)

	return res
```

### avoiding floating point division (and a hashmap)

The issue with the solution above is that doing floating point division to find the slope was causing some issues with points not being detected on lines. Instead, we should just maintain the $\delta x$ and $\delta y$ values for each point relative to an anchor point. If we simplify these fractions, then any points that share simplified deltas will like on the same line relative to our anchor point.

We iterate through $n$ anchor points, and for every other point, calculate it’s simplified deltas and store it in a counter hashmap.

Make sure to account for two edge cases:

1. If we see another value equal to our anchor point, that is present on _every_ line using our anchor point.
2. If we see another value with the same $x$ value, then that is on the vertical line with our anchor point, and we should store it separately as simplifying the fraction with GCD will lead to division by zero.

```python
from math import gcd

  

class Solution:

def maxPoints(self, points: List[List[int]]) -> int:

"""

brute force:

- for each point, take another point and then try to find all other points

on that line

(1,1)

(3,2)

(5,3)

  

1. solve for slope

m = (2-1)/(3-1) = 1/2

  

2. solve for intercept

1 = 1/2(1) + b

b = 1/2

  

# test every other point to see if it

# satisfies this equation

y = 0.5x + 0.5

  

there are n^2 pairs of points, each pair takes O(n) -> O(n^3)

"""

# simplify the fraction

def gcd_simplify(x, y):

g = gcd(x, y)

return x // g, y // g

if len(points) < 3:

return len(points)

  

res = 0

for i in range(len(points)):

x1, y1 = points[i]

slopes = defaultdict(int)

dupes = 1 # point itself is in every slope

vertical = 0

for j in range(i+1, len(points)):

x2, y2 = points[j]

  

# vertical line

if x1 == x2 and y1 == y2:

dupes += 1

elif x1 == x2:

vertical += 1

else:

dx = x2 - x1 if x2 > x1 else x1-x2

dy = y2 - y1 if x2 > x1 else y1-y2

slope = gcd_simplify(dy, dx)

slopes[slope] += 1

  

local_best = vertical

if slopes:

local_best = max(local_best, max(slopes.values()))

res = max(res, local_best + dupes)

  

return res
```
