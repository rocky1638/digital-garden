---
type: leetcode
title: 236. lowest common ancestor of a binary tree
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/
date: 2022-11-12
updated: 2024-08-28
tags:
  - recursion
  - dfs
  - binary-tree
---

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

## solution

At each step in the recursion through the binary tree, we will return whether the current node has `p` and `q` as descendants. We do this by first recursing on the children of the current node (post-order traversal).

Because we recurse on the children first, the first node that we reach that satisfies `has_q` and `has_p` must be the lowest common ancestor.

```python
def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
	res = None
	  
	def dfs(node):
		nonlocal res
		if not node:
			return False, False

		l_has_p, l_has_q = dfs(node.left)
		r_has_p, r_has_q = dfs(node.right)
		  
		has_p = node == p or l_has_p or r_has_p
		has_q = node == q or l_has_q or r_has_q
		  
		if has_p and has_q and res is None:
			res = node
		return has_p, has_q

	dfs(root)
	return res
```
