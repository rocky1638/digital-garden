---
type: leetcode
title: "2013. detect squares"
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-05-15
---

You are given a stream of points on the X-Y plane. Design an algorithm that:

- **Adds** new points from the stream into a data structure. **Duplicate** points are allowed and should be treated as different points.
- Given a query point, **counts** the number of ways to choose three points from the data structure such that the three points and the query point form an **axis-aligned square** with **positive area**.

An **axis-aligned square** is a square whose edges are all the same length and are either parallel or perpendicular to the x-axis and y-axis.

Implement the `DetectSquares` class:

- `DetectSquares()` Initializes the object with an empty data structure.
- `void add(int[] point)` Adds a new point `point = [x, y]` to the data structure.
- `int count(int[] point)` Counts the number of ways to form **axis-aligned squares** with point `point = [x, y]` as described above.

## solution

First, we store all of the points that are added into a frequency dictionary.

There are two options for finding squares when given a point.

1. We can try to form a horizontal/vertical line, and then look to either side to try to find another horizontal/vertical line that is equidistant away, such that four points form a square.
2. Alternatively, we can look for two points on a diagonal such that the difference in $x$ and $y$ values between the two points are the same. Then, we know the other two points must lie on the perpindicular diagonal.

Finally, given duplicate points, we know that we can form any combination of squares with duplicate points, and such the frequencies are multiplied to count the total number of squares that can be made with four given points.

```python
class DetectSquares:
	def __init__(self):
		self.freq = Counter()
	
	def add(self, point: List[int]) -> None:
		self.freq[tuple(point)] += 1
	
	def count(self, point: List[int]) -> int:
		ans = 0
		# first, try to form horizontal lines (other values that share x)
		x1, y1 = point
		for (x3, y3), cnt in self.freq.items():
			# find pairs of points such that they are
			# diagonally equidistant
			if abs(x1-x3) == 0 or abs(x1-x3) != abs(y1-y3):
				continue
			ans += cnt * self.freq[(x1, y3)] * self.freq[(x3, y1)]
			return ans
```
