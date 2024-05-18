---
type: leetcode
title: 1035. uncrossed lines
tags:
  - backtracking
  - dp
aliases: 
parents: 
children: 
supports:
  - "[[72-edit-distance]]"
enemies: 
date: 2022-12-30
updated: 2024-04-20
---

You are given two integer arrays `nums1` and `nums2`. We write the integers of `nums1` and `nums2` (in the order they are given) on two separate horizontal lines.

We may draw connecting lines: a straight line connecting two numbers `nums1[i]` and `nums2[j]` such that:

- `nums1[i] == nums2[j]`, and
- the line we draw does not intersect any other connecting (non-horizontal) line.

Note that a connecting line cannot intersect even at the endpoints (i.e., each number can only belong to one connecting line).

Return _the maximum number of connecting lines we can draw in this way_.

## solutions

### recursion with memoization

The main starting intuition here begins with how we would have overlapping lines.

Say we index into `nums1` with index $i$ and `nums2` with index $j$. Then, if we create a connection between indices $i$ and $j$, the two ways we can create overlap is if the next connection, say $i^\prime$ and $j^\prime$, satisfy $i^\prime \lt i \land j^\prime \gt j$ or $i^\prime \gt i \land j^\prime \lt j$.

So, this means that if we always iterate forward with $i$ and $j$, we’ll never create any overlapping lines. Furthermore, we can enumerate all possible valid scenarios by exploring the decision tree. At each step, we can advance, $i$, $j$, or both.

```python
def maxUncrossedLines(self, nums1: List[int], nums2: List[int]):
	memo = {}

	def recurse(i, j):
		if i == len(nums1) or j == len(nums2):
			return 0
	  
		if (i, j) in memo:
			return memo[(i,j)]
	  
		connect = 0
		if nums1[i] == nums2[j]:
			connect = recurse(i+1, j+1) + 1
	  
		no_connect = max(
			recurse(i, j+1),
			recurse(i+1, j)
		)
	  
		memo[(i,j)] = max(connect, no_connect)
		return memo[(i,j)]

	return recurse(0, 0)
```

### dynamic programming

We can pretty simply convert the above solution into a 2D dynamic programming solution.

```python
def maxUncrossedLines(self, nums1: List[int], nums2: List[int]):
	dp = [[0 for _ in range(len(nums2)+1)] for _ in range(len(nums1)+1)]
	  
	for i in reversed(range(len(nums1))):
		for j in reversed(range(len(nums2))):
			if nums1[i] == nums2[j]:
				dp[i][j] = dp[i+1][j+1] + 1
			else:
				dp[i][j] = max(
					dp[i+1][j],
					dp[i][j+1]
				)

	return dp[0][0]
```
