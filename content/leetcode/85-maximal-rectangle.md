---
type: leetcode
title: 85. maximal rectangle
tags:
  - monotonic-stack
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-22
---

Given a `rows x cols` binary `matrix` filled with `0`'s and `1`'s, find the largest rectangle containing only `1`'s and return _its area_.

## solution

At first, I felt that this question was very similar to [[221-maximal-square]], and tried to figure out a way to solve it in the same way using dynamic programming.

However, I quickly realized that the recursive relationship on “best square anchored at index” is a lot simpler than “best rectangle anchored at index”. This is because to optimize for the largest area rectangle, we’d have to store every possible rectangle anchored at each index, as we don’t know ahead of time which rectangle will work best with other rectangles to form a bigger rectangle.

---

Instead, the question to think about here is [[84-largest-rectangle-in-histogram]]. Once you make this connection, we realize we can just treat each increasing vertical slice of the matrix as a histogram.

Note that we don’t need to consider bands of histogram in the middle, as the answer will always be equal or better if we expand our band to the top.

```python
def largestRectangleSoFar(self, heights) -> int:
	stack = []
	ans = 0
	  
	for i, h in enumerate(heights):
		prev_idx = None
		while stack and stack[-1][0] > h:
			popped, prev_idx = stack.pop()
			ans = max(ans, popped * (i-prev_idx))
	  
		if h > 0:
			if prev_idx is not None:
				stack.append((h, prev_idx))
			else:
				stack.append((h, i))
	  
	n = len(heights)
	for h, i in stack:
		ans = max(ans, (n-i)*h)
	  
	return ans
  

def maximalRectangle(self, matrix: List[List[str]]) -> int:
	heights = [int(x) for x in matrix[0]]
	ans = self.largestRectangleSoFar(heights)
	  
	for i in range(1, len(matrix)):
		for j in range(len(matrix[i])):
			heights[j] = heights[j] + int(matrix[i][j]) if matrix[i][j] == "1" else 0
	  
		ans = max(ans, self.largestRectangleSoFar(heights))
	return ans
```
