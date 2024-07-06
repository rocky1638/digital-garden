---
type: <% tp.file.cursor() %>
title: <% tp.file.cursor() %>
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-06-11
---

For a binary tree **T**, we can define a **flip operation** as follows: choose any node, and swap the left and right child subtrees.

A binary tree **X** is _flip equivalent_ to a binary tree **Y** if and only if we can make **X** equal to **Y** after some number of flip operations.

Given the roots of two binary trees `root1` and `root2`, return `true` if the two trees are flip equivalent or `false` otherwise.

## solution

We realize that for any two trees to be flip equivalent, they need to satisfy two properties:

1. The root nodes have to match.
2. The two subtrees have to be flip equivalent (we must consider both cases when we flip at this node or not).

```python
def flipEquiv(self, root1: Optional[TreeNode], root2: Optional[TreeNode]):
	if root1 is None and root2 is None:
		return True
	  
	if root1 is None or root2 is None:
		return False
	  
	if root1.val != root2.val:
		return False
	  
	
	no_flip_result = self.flipEquiv(root1.left, root2.left) and self.flipEquiv(
		root1.right, root2.right
	)
	flip_result = self.flipEquiv(root1.left, root2.right) and self.flipEquiv(
		root1.right, root2.left
	)
	  
	return no_flip_result or flip_result
```
