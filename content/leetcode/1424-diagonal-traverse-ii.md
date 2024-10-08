---
type: leetcode
title: 1424. diagonal traverse ii
tags:
  - hashmap
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-09-09
---

Given a 2D integer array `nums`, return _all elements of_ `nums` _in diagonal order as shown in the below images_.

## solutions

### group values by diagonal

```python
def findDiagonalOrder(self, nums: List[List[int]]) -> List[int]:
	groups = defaultdict(list)
	for i in reversed(range(len(nums))):
		for j in range(len(nums[i])):
			groups[i+j].append(nums[i][j])

	out = []
	i = 0
	while i in groups:
		out.extend(groups[i])
		i += 1
	return out
```

### elegant bfs

![[1424-diagonal-traverse-ii-bfs.png]]

![[1424-diagonal-traverse-ii.png]]

```python
def findDiagonalOrder(self, nums: List[List[int]]) -> List[int]:
	queue = deque([(0, 0)])
	ans = []
	
	while queue:
		row, col = queue.popleft()
		ans.append(nums[row][col])
	
		if col == 0 and row + 1 < len(nums):
			queue.append((row + 1, col))
	
		if col + 1 < len(nums[row]):
			queue.append((row, col + 1))
	
	return ans
```
