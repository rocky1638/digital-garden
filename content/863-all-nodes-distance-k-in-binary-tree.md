---
type: leetcode
title: 863. all nodes distance k in binary tree
tags:
  - dfs
  - bfs
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-16
updated: 2024-09-16
---

Given the `root` of a binary tree, the value of a target node `target`, and an integer `k`, return _an array of the values of all nodes that have a distance_ `k` _from the target node._

You can return the answer in **any order**.

![[863-all-nodes-distance-k-in-binary-tree.png]]

## solution

We do a traversal to get parent pointers for every node. Then, we can simply traverse the tree like a normal graph from the target node.

```python
def distanceK(self, root: TreeNode, target: TreeNode, k: int) -> List[int]:
	# generate parent pointers
	parents = {}
	def dfs(node, parent):
		parents[node.val] = parent
	  
		if node.left:
			dfs(node.left, node)
		if node.right:
			dfs(node.right, node)
	dfs(root, None)

	# BFS from target node
	res = []
	q = deque([(target, 0)])
	visited = set([target.val])
	while q:
		cur, depth = q.popleft()
	  
		if depth == k:
			res.append(cur.val)
		if depth > k:
			break
	  
		for neighbor in [parents[cur.val], cur.left, cur.right]:
			if neighbor and neighbor.val not in visited:
				visited.add(neighbor.val)
				q.append((neighbor, depth+1))
	return res
```
