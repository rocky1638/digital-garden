---
type: leetcode
title: 1609. even odd tree
tags:
  - binary-tree
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-10
updated: 2024-09-10
---

A binary tree is named **Even-Odd** if it meets the following conditions:

- The root of the binary tree is at level index `0`, its children are at level index `1`, their children are at level index `2`, etc.
- For every **even-indexed** level, all nodes at the level have **odd** integer values in **strictly increasing** order (from left to right).
- For every **odd-indexed** level, all nodes at the level have **even** integer values in **strictly decreasing** order (from left to right).

Given the `root` of a binary tree, _return_ `true` _if the binary tree is **Even-Odd**, otherwise return_ `false`_._

## solution

Pretty straightforward level-order traversal while following the extra rules. Keep a `prev` value to make sure the increasing/decreasing rules are met.

```python
def isEvenOddTree(self, root: Optional[TreeNode]) -> bool:
	q = deque([root])
	level = 0
	
	def valid(val, prev, level):
		if not prev:
			return (val-level) % 2 == 1
	
		if level & 1:
			return val < prev and val % 2 == 0
		return val > prev and val & 1
	
	while q:
		level_len = len(q)
		prev = None
	
		for _ in range(level_len):
			cur = q.popleft()
			if not valid(cur.val, prev, level):
				return False
			prev = cur.val
	
			if cur.left: 
				q.append(cur.left)
			if cur.right: 
				q.append(cur.right)
	
		level += 1
	return True
```
