---
type: leetcode
title: 333. largest bst subtree
tags:
  - recursion
  - binary-tree
  - binary-search-tree
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-13
updated: 2024-09-14
---

Given the root of a binary tree, find the largest subtree, which is also a Binary Search Tree (BST), where the largest means subtree has the largest number of nodes.

A **Binary Search Tree (BST)** is a tree in which all the nodes follow the below-mentioned properties:

- The left subtree values are less than the value of their parent (root) node's value.
- The right subtree values are greater than the value of their parent (root) node's value.

**Note:** A subtree must include all of its descendants.

## solutions

### preorder recursion w/ validation

We can first check to see if the BST rooted at `root` is a valid BST (we can do this by propagating valid left and right bounds down the recursion).

The issue with this preorder recursion is that we do a lot of repeated work, as the first call checks every node, but each subsequent call has to recalculate all of those nodes.

```python
# O(n)
def is_valid_bst(self, node, l, r) -> bool:
	if not node:
		return True
	return (
		l < node.val < r
		and self.is_valid_bst(node.left, l, node.val)
		and self.is_valid_bst(node.right, node.val, r)
	)

# O(n)
def count_nodes(self, node):
	if not node:
		return 0
	return 1 + self.count_nodes(node.left) + self.count_nodes(node.right)

# best case: O(nlogn), worst case: O(n^2)
def largestBSTSubtree(self, root: Optional[TreeNode]) -> int:
	if not root:
		return 0

	# If current subtree is a valid BST, its our best answer.
	if self.is_valid_bst(root, -inf, inf):
		return self.count_nodes(root)

	# Find BST in left and right subtrees of current nodes.
	return max(
		self.largestBSTSubtree(root.left),
		self.largestBSTSubtree(root.right)
	)
```

### postorder validation

To save on computation, we should start by computing the nested values first. For example, if we already know that a node’s left and right children are valid BST’s (as well as their ranges), we can check whether `node` is a valid BST in constant time.

This is very similar in logic to the postorder optimization reached in [[427-construct-quad-tree]].

```python
# O(n) - we only traverse each node once
def largestBSTSubtree(self, root: Optional[TreeNode]) -> int:
	def helper(node):
		if not node:
			# min = inf, max = -inf
			# this ensures it's a valid child for any node
			return 0, inf, -inf
		  
		left_size, left_min, left_max = helper(node.left)
		right_size, right_min, right_max = helper(node.right)
		  
		# node is a valid BST
		if left_max < node.val < right_min:
			# handle leaf workaround, if left_min is inf or right_max is -inf, use root.val
			return 1+left_size+right_size, min(node.val, left_min), max(node.val, right_max)

		# node is not a valid BST
		# largest BST in node's subtree is best of left or right recursion
		# if neither left or right are valid BST, the recursion keeps going down
		# min = -inf, max = inf -- invalid as child for any node
		return max(left_size, right_size), -inf, inf
	  
	ans, _, _ = helper(root)
	return ans
```
