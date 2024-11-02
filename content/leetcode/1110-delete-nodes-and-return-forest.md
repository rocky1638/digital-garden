---
type: leetcode
title: 1110. delete nodes and return forest
tags:
  - binary-tree
  - recursion
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-10-17
---

Given the `root` of a binary tree, each node in the tree has a distinct value.

After deleting all nodes with a value in `to_delete`, we are left with a forest (a disjoint union of trees).

Return the roots of the trees in the remaining forest. You may return the result in any order.

## solution

We traverse down the tree, and keep track of tree roots that we want to return. The key is that when we remove a node `a`, it’s children `b` and `c` temporarily become tree roots in the forest.

We add these to `roots`, and then traverse down to them. In the case that either `b` or `c` are also to be deleted, we can remove them again from `roots` and continue traversing.

In order to effectively clear references, we pass in a reference to the parent node in the recursion.

```python
def delNodes(self, root: Optional[TreeNode], to_delete: List[int]):
	roots = set([root])
	
	def dfs(node, p, d):
		if not node:
			return
		
		if node.val not in to_delete:
			dfs(node.left, node, "l") 
			dfs(node.right, node, "r")
		else:
			if node in roots:
				roots.remove(node)
		
			left, right = node.left, node.right
			if left: roots.add(left)
			if right: roots.add(right)
		
			# clear reference of parent
			if d == "l" and p:
				p.left = None
			if d == "r" and p:
				p.right = None
		
			# delete node
			del node
		
			dfs(left, None, "l")
			dfs(right, None, "r")
	
	dfs(root, None, "l")
	return roots
```

Another way to think about it is here.

We do a preorder traversal (DFS) down the tree. If a node is to be deleted, update the reference to the parent.

Note that if the node is being deleted, we don’t need to worry about if its parent is being deleted (normally if its parent was being deleted, it would be a new root, but instead, we’re deleting it).

So, if we’re not deleting a node, we can check if the parent is being deleted (this is the only condition that allows the current node to be a new root).

```python
def delNodes(self, root: Optional[TreeNode], to_delete: List[int]) -> List[TreeNode]:
	tds = set(to_delete)
	res = []

	def dfs(node, parent, is_left):
		if not node:
			return
		  
		if node.val in tds:
			if parent:
				if is_left:
					parent.left = None
				else:
					parent.right = None

		elif parent is None or parent.val in tds:
			res.append(node)
		  
		dfs(node.left, node, True)
		dfs(node.right, node, False)
		  
	dfs(root, None, False)
	return res
```
