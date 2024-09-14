---
type: leetcode
title: 426. convert binary tree to sorted doubly linked list
tags:
  - dfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-30
updated: 2024-08-30
---

Convert a **Binary Search Tree** to a sorted **Circular Doubly-Linked List** in place.

You can think of the left and right pointers as synonymous to the predecessor and successor pointers in a doubly-linked list. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.

We want to do the transformation **in place**. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. You should return the pointer to the smallest element of the linked list.

## solutions

We first DFS all the way down to find the largest value in the left subtree and the smallest value in the right subtree. These will be predecessor/successor of `node`. Because we don’t want to make our recursive call dependent on direction, just return both min and max.

Then, since we’ve already done all the traversals lower down in the tree by the time we return from the recursive call, we can change the pointers to make our DLL.

```python
def treeToDoublyList(self, root: 'Optional[Node]') -> 'Optional[Node]':
	if not root:
		return root
	  
	# dfs returns max and min with node as root
	def dfs(node):
		if not node:
			return None, None
	  
		lmin, rmax = None, None
		if node.left:
			lmin, lmax = dfs(node.left)
			node.left = lmax
			lmax.right = node
	  
		if node.right:
			rmin, rmax = dfs(node.right)
			node.right = rmin
			rmin.left = node
	  
		mn = lmin if lmin else node
		mx = rmax if rmax else node
		return mn, mx

	mn, mx = dfs(root)

	# make circular
	mn.left = mx
	mx.right = mn
	  
	return mn
```

A more elegant solution is to just keep a single variable, `last`, which tracks the previous node we’ve seen in the in-order traversal. Because we’re traversing in-order, we can always just link current node to `last`.

```python
def treeToDoublyList(self, root: 'Node') -> 'Node':
	def helper(node):
		"""
		Performs standard inorder traversal:
		left -> node -> right
		and links all nodes into DLL
		"""
		nonlocal last, first
		if node:
			# left
			helper(node.left)
	
			# node 
			if last:
				# link the previous node (last)
				# with the current one (node)
				last.right = node
				node.left = last
			else:
				# keep the smallest node
				# to close DLL later on
				# this case ONLY happens for smallest node
				first = node        
			last = node
	
	# right
	helper(node.right)
	
	if not root:
		return None
	
	# the smallest (first) and the largest (last) nodes
	first, last = None, None
	helper(root)
	
	# close DLL
	last.right = first
	first.left = last
	return first
```
