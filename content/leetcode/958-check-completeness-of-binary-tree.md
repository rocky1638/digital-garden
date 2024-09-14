---
type: leetcode
title: 958. check completeness of binary tree
tags:
  - binary-tree
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-19
---

Given the `root` of a binary tree, determine if it is a _complete binary tree_.

In a **[complete binary tree](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)**, every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between `1` and `2h` nodes inclusive at the last level `h`.

## solution

The intuition to perform a level-order traversal is pretty straightforward here.

The next and second thought to solve this problem is to realize that once we visit a `null` node, we cannot then see another non-null node, as that would mean our tree is incomplete.

```python
def isCompleteTree(self, root: Optional[TreeNode]) -> bool:
	q = deque([root])
	none_seen = False
	  
	while q:
		cur = q.popleft()
	  
		if cur is None:
			none_seen = True
			continue
		if cur and none_seen:
			return False
	  
		q.append(cur.left)
		q.append(cur.right)

	return True
```
