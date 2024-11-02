---
type: leetcode
title: 654. maximum binary tree
tags:
  - recursion
  - binary-tree
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-28
updated: 2024-10-28
---

You are given an integer array `nums` with no duplicates. A **maximum binary tree** can be built recursively from `nums` using the following algorithm:

1. Create a root node whose value is the maximum value in `nums`.
2. Recursively build the left subtree on the **subarray prefix** to the **left** of the maximum value.
3. Recursively build the right subtree on the **subarray suffix** to the **right** of the maximum value.

Return _the **maximum binary tree** built from_ `nums`.

## solution

```python
# O(nlogn), worst case O(n^2) in linked list case
def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
	n = len(nums)
	def construct(l, r):
		if l > r:
			return None
	  
		max_seen = -inf
		idx = -1
		for i in range(l, r+1):
			if nums[i] > max_seen:
				max_seen = nums[i]
				idx = i
		root = TreeNode(max_seen)
		root.left = construct(l, idx-1)
		root.right = construct(idx+1, r)
		return root
	  
	return construct(0, n-1)
```
