---
type: leetcode
title: 536. construct binary tree from string
tags:
  - string
  - recursion
  - binary-tree
aliases: 
parents: 
children: 
supports:
  - "[[224-basic-calculator]]"
enemies: 
date: 2024-10-02
updated: 2024-10-02
---

You need to construct a binary tree from a string consisting of parenthesis and integers.

The whole input represents a binary tree. It contains an integer followed by zero, one or two pairs of parenthesis. The integer represents the root's value and a pair of parenthesis contains a child binary tree with the same structure.

You always start to construct the **left** child node of the parent first if it exists.

## solution

We parse through the string, and enter a recursion when we see an opening bracket. Whenever `i` lands on a closing bracket, we know we can exit the recursion (because if a node has two children, the recursive call for the left child will return the index of the next opening bracket for the right child).

```python
# O(n)
def str2tree(self, s: str) -> Optional[TreeNode]:
	def recurse(idx):
		if idx == len(s):
			return None, idx

		neg = False
		node = None
		left_child_found = False
		i = idx
		  
		while i < len(s):
			char = s[i]
		  
			if char == "-":
				neg = True
				i += 1
			elif char == "(":
				if left_child_found:
					node.right, i = recurse(i+1)
				else:
					node.left, i = recurse(i+1)
					left_child_found = True
			elif char == ")":
				return node, i+1
			else:
				if not node:
					node = TreeNode(-int(char) if neg else int(char))
				else:
					node.val *= 10
					if neg:
						node.val -= int(char)
					else:
						node.val += int(char)
				i += 1

		return node, i

	root, _ = recurse(0)
	return root
```
