---
type: leetcode
title: 2265. count nodes equal to average of subtree
tags:
  - binary-tree
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-23
---

Given the `root` of a binary tree, return _the number of nodes where the value of the node is equal to the **average** of the values in its **subtree**_.

**Note:**

- The **average** of `n` elements is the **sum** of the `n` elements divided by `n` and **rounded down** to the nearest integer.
- A **subtree** of `root` is a tree consisting of `root` and all of its descendants.

## solution

Pretty basic recursion, we just return the sum and size of each subtree.

```python
def averageOfSubtree(self, root: TreeNode) -> int:
	ans = 0
	  
	def recurse(node):
		nonlocal ans
		if not node:
			return (0, 0)
	  
		sum_left, size_left = recurse(node.left)
		sum_right, size_right = recurse(node.right)
	  
		total_sum = node.val + sum_left + sum_right
		total_size = 1 + size_left + size_right
		avg = total_sum // total_size
		if avg == node.val:
			ans += 1
		return total_sum, total_size

	recurse(root)
	return ans
```
