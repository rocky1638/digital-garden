---
type: leetcode
title: 145. binary tree postorder traversal
tags:
  - stack
  - recursion
  - binary-tree
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-09-10
---

Given the `root` of a binary tree, return _the postorder traversal of its nodes' values_.

## solutions

### recursive

```python
def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
	out = []
	def post(node):
		if not node:
			return
		post(node.left)
		post(node.right)
		out.append(node.val)
	
	post(root)
	return out
```

### iterative

```python
def postorder_traversal_iteratively(self, root: 'TreeNode'):
	if not root:
		return []
	stack, res = [root], []
	# used to record whether left or right child has been visited
	last = None
	while stack:
		root = stack[-1]
		# if current node has no left right child, or left child or right child has been visited, then process and pop it
		# if last is root.right or root.left, that means root has already gone through the else case, meaning we've already processed right and left (if one/both of them exist)
		if not root.left and not root.right or last and (root.left == last or root.right == last):
			res.append(root.val)
			stack.pop()
			last = root

		# if not, push right and left child in stack
		else: # push right first because of FILO
			if root.right:
				stack.append(root.right)
			if root.left:
				stack.append(root.left) return res
```
