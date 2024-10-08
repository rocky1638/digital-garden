---
type: leetcode
title: 270. closest binary search tree value
tags:
  - binary-search
  - binary-search-tree
  - greedy
  - dfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-31
---

Given the `root` of a binary search tree and a `target` value, return _the value in the BST that is closest to the_ `target`. If there are multiple answers, print the smallest.

## solutions

### inorder traversal

We can inorder traverse the BST, and return once the absolute diff starts increasing. This means we’ve passed the closest value and are moving away now.

```python
def closestValue(self, root: Optional[TreeNode], target: float) -> int:
	ans = None
	best_diff = inf
	  
	def inorder(node):
		nonlocal best_diff, ans
		if not node:
			return
	  
		# go left first
		inorder(node.left)
	  
		# handle node
		diff = abs(node.val-target)
	  
		# break early once abs(diff) starts increasing
		if diff >= best_diff:
			return
		else:
			best_diff = diff
			ans = node.val

		# go right
		inorder(node.right)
	
	return ans
```

### binary search

We can actually just always greedily binary search towards the `target`. Without loss of generality, if `target > node.val`, we know for certain that `target` is closer to `node.val` than it is to any node in `node.left`. So, we can greedily go right.

```python
def closestValue(self, root: TreeNode, target: float) -> int:
	closest = root.val
	while root:
		closest = min(
			root.val, closest, key = lambda x: (abs(target - x), x)
		)
		root = root.left if target < root.val else root.right
	return closest
```
