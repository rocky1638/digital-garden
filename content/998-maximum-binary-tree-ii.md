---
type: leetcode
title: 998. maximum binary tree ii
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

A **maximum tree** is a tree where every node has a value greater than any other value in its subtree.

You are given the `root` of a maximum binary tree and an integer `val`.

Just as in the [previous problem](https://leetcode.com/problems/maximum-binary-tree/), the given tree was constructed from a list `a` (`root = Construct(a)`) recursively with the following `Construct(a)` routine:

- If `a` is empty, return `null`.
- Otherwise, let `a[i]` be the largest element of `a`. Create a `root` node with the value `a[i]`.
- The left child of `root` will be `Construct([a[0], a[1], ..., a[i - 1]])`.
- The right child of `root` will be `Construct([a[i + 1], a[i + 2], ..., a[a.length - 1]])`.
- Return `root`.

Note that we were not given `a` directly, only a root node `root = Construct(a)`.

Suppose `b` is a copy of `a` with the value `val` appended to it. It is guaranteed that `b` has unique values.

Return `Construct(b)`.

## solution

Because we want to simulate as if the new value was at the end of the list, if it’s not going to be the new `root`, it _must_ be inserted into the right subtree.

```python
def insertIntoMaxTree(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
	def insert(node):
		if not node:
			return TreeNode(val)
  
		# val must be root of all remaining nodes
		if val > node.val:
			new_node = TreeNode(val)
			new_node.left = node
			return new_node
		node.right = insert(node.right)
		return node

	return insert(root)
```
