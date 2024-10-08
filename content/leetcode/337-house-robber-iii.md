---
type: leetcode
title: 337. house robber iii
tags:
  - binary-tree
  - dp
  - recursion
  - memoization
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-16
updated: 2024-08-16
---

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called `root`.

Besides the `root`, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if **two directly-linked houses were broken into on the same night**.

Given the `root` of the binary tree, return _the maximum amount of money the thief can rob **without alerting the police**_.

## solutions

### recursion w/ memoization

Questions involving trees lend themselves to recursion, and there’s no exception here. The decision to be made at each node is whether to rob the house or not.

Keep track of whether the parent was robbed in the recursive call. Memoize with a map to avoid duplicated work.

```python
def rob(self, root: Optional[TreeNode]) -> int:
	memo = {}
	def recurse(node, parent_robbed):
		if not node:
		return 0
	  
		if (node, parent_robbed) in memo:
			return memo[(node, parent_robbed)]

		# don't rob current node
		best = recurse(node.left, False) + recurse(node.right, False)

		# rob current node
		if not parent_robbed:
		best = max(
			best,
			node.val + recurse(node.left, True) + recurse(node.right, True)
		)
		memo[(node, parent_robbed)] = best
		return best
	  
	return recurse(root, False)
```

### dp

The dynamic programming approach here is weird because we first need to represent the tree as an array. We can do this with a level-order traversal with a BFS, and then use a hashmap to keep a map of parent to children nodes.

```python
def rob(self, root: TreeNode) -> int:
	if not root:
		return 0
	
	# reform tree into array-based tree
	tree = []
	graph = defaultdict(list)
	index = -1
	q = [(root, -1)]
	while q:
		node, parent_index = q.pop(0)
		if node:
			index += 1
			tree.append(node.val)
			graph[index] = []
			graph[parent_index].append(index)
			q.append((node.left, index))
			q.append((node.right, index))
	
	# represent the maximum start by node i with robbing i
	dp_rob = [0] * (index+1)
	
	# represent the maximum start by node i without robbing i
	dp_not_rob = [0] * (index+1)
	
	for i in reversed(range(index+1)):
		if not graph[i]:  # if is leaf
			dp_rob[i] = tree[i]
			dp_not_rob[i] = 0
		else:
			dp_rob[i] = tree[i] + sum(dp_not_rob[child]
			for child in graph[i])
				dp_not_rob[i] = sum(max(dp_rob[child], dp_not_rob[child] for child in graph[i])
	
	return max(dp_rob[0], dp_not_rob[0])
```
