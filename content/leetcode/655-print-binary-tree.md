---
type: leetcode
title: 655. print binary tree
tags:
  - binary-tree
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-22
---

Given the `root` of a binary tree, construct a **0-indexed** `m x n` string matrix `res` that represents a **formatted layout** of the tree. The formatted layout matrix should be constructed using the following rules:

- The **height** of the tree is `height` and the number of rows `m` should be equal to `height + 1`.
- The number of columns `n` should be equal to `2height+1 - 1`.
- Place the **root node** in the **middle** of the **top row** (more formally, at location `res[0][(n-1)/2]`).
- For each node that has been placed in the matrix at position `res[r][c]`, place its **left child** at `res[r+1][c-2height-r-1]` and its **right child** at `res[r+1][c+2height-r-1]`.
- Continue this process until all the nodes in the tree have been placed.
- Any empty cells should contain the empty string `""`.

Return _the constructed matrix_ `res`.

## solution

This is mostly a math problem. We figure out the height of the tree, then find the formulas for how to calculate the indices of left and right child given the current level and index.

```python
def printTree(self, root: Optional[TreeNode]) -> List[List[str]]:
	def getHeight(node):
		if not node:
			return 0
		if node:
			return 1 + max(getHeight(node.right), getHeight(node.left))
	  
	h = getHeight(root)
	w = 2**h-1
	ret = [[""]*w for i in range(h)]
	  
	def recurse(node, level, index):
		nonlocal ret
		if not node:
			return
	  
		ret[level-1][index] = str(node.val)
	  
		recurse(node.left, level+1, index-(2**(h-level-1)))
		recurse(node.right, level+1, index+(2**(h-level-1)))
	  
	recurse(root, 1, (w-1)//2)
	return ret
```
