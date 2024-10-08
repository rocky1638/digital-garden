---
type: leetcode
title: 450. delete node in a bst
tags:
  - binary-search-tree
  - recursion
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-15
updated: 2024-08-15
---

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return _the **root node reference** (possibly updated) of the BST_.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

## solution

Pretty tough to figure out without past experience. It’s helpful to break the problem into several pieces, starting with two main subproblems:

1. Find the node that needs to be deleted. If the node doesn’t exist, then don’t change anything. We can do this recursively.
2. Once we find the node to be deleted, what do we do?
	1. If it’s a leaf node, just make it `None`.
	2. If there’s only one child, just replace the node to be deleted with it’s one child, because that child BST is guaranteed to be valid (satisfy BST constraints) as a replacement for the deleted node.

Finally, let’s consider the crux of the problem, what happens when there’s two children trees. Assume for now, without loss of generality, that we’re going to promote a node from the right subtree into the deleted node $d$’s spot.

Note that the only node that can be chosen as this replacement is the successor node, or the smallest value in the right subtree. This is because after the swap, all other nodes of the right subtree $R$ will be to the right of this replacement node $r$, so by BST rules, must be greater. If we choose any value other than the smallest value in $R$, some value will remain in $R$, $r’$, that is smaller than $r$ but is to the right of $r$.

The same can apply to doing the left subtree, but we want the predecessor, or the largest value in the left subtree.

The “clever” part is that after the replacement, we can recursively remove this now duplicated value $r$ from the subtree.

```python
def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
	if not root:
		return root

	# "minimum value in right tree"
	def successor(node):
		node = node.right
		while node.left:
			node = node.left
		return node

	# "maximum value in left tree"
	def predecessor(node):
		node = node.left
		while node.right:
			node = node.right
		return node

	if root.val < key:
		root.right = self.deleteNode(root.right, key)
	elif root.val > key:
		root.left = self.deleteNode(root.left, key)
	else:
		if not root.left and not root.right:
			root = None
		elif not root.right:
			root.val = predecessor(root).val
			root.left = self.deleteNode(root.left, root.val)
		else:
			root.val = successor(root).val
			root.right = self.deleteNode(root.right, root.val)
	return root
```

## references

- https://www.youtube.com/watch?v=LFzAoJJt92M
