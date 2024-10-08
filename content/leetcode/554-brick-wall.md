---
type: leetcode
title: 554. brick wall
tags:
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-03
updated: 2024-10-03
---

There is a rectangular brick wall in front of you with `n` rows of bricks. The `ith` row has some number of bricks each of the same height (i.e., one unit) but they can be of different widths. The total width of each row is the same.

Draw a vertical line from the top to the bottom and cross the least bricks. If your line goes through the edge of a brick, then the brick is not considered as crossed. You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.

Given the 2D array `wall` that contains the information about the wall, return _the minimum number of crossed bricks after drawing such a vertical line_.

## solution

Pretty basic logic solution if you draw it out.

```python
def leastBricks(self, wall: List[List[int]]) -> int:  
	"""  
	want to find area with most edges of bricks  
	[1,2,2,1] -> [1,3,5]  
	[3,1,2] -> [3,4]  
	[1,3,2] -> [1,4]  
	"""  
	best_freq = 0   
	counts = Counter()  
	for row in wall:  
		acc = 0  
		for length in row[:-1]:  
			acc += length  
			counts[acc] += 1  
			best_freq = max(best_freq, counts[acc])  

	return len(wall) - best_freq
```
