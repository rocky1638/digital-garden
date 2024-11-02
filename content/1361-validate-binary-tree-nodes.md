---
type: leetcode
title: 1361. validate binary tree nodes
tags:
  - dfs
  - bfs
  - binary-tree
  - union-find
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-08
updated: 2024-10-08
---

You have `n` binary tree nodes numbered from `0` to `n - 1` where node `i` has two children `leftChild[i]` and `rightChild[i]`, return `true` if and only if **all** the given nodes form **exactly one** valid binary tree.

If node `i` has no left child then `leftChild[i]` will equal `-1`, similarly for the right child.

Note that the nodes have no values and that we only use the node numbers in this problem.

## solutions

From a high level, we know that a valid tree satisfies the following conditions:

1. There is one root, with an indegree of zero. Every other node must have an indegree of one (one parent).
2. The whole tree is connected.
3. No cycles.

### bfs

We go through all of the children and remove them from the list of candidates for root. If we don’t end up with a single root, return early.

Else, we just BFS/DFS using the root, and return early if we ever see a node we’ve already processed (cycle exists).

Finally, ensure that the graph is fully connected (we saw every node in our traversal).

```python
def validateBinaryTreeNodes(self, n: int, leftChild: List[int], rightChild: List[int]) -> bool:
	nodes = {i for i in range(n)}
	non_child_nodes = set()
	for i in range(n):
		if leftChild[i] > -1:
			non_child_nodes.add(leftChild[i])
		if rightChild[i] > -1:
			non_child_nodes.add(rightChild[i])

	# there doesn't exist a unique root
	remaining_nodes = list(nodes - non_child_nodes)
	if len(remaining_nodes) != 1:
		return False

	seen = set([remaining_nodes[0]])
	q = deque([remaining_nodes[0]])
	  
	while q:
		cur = q.popleft()
	  
		if leftChild[cur] > -1:
			if leftChild[cur] in seen:
				return False
			q.append(leftChild[cur])
			seen.add(leftChild[cur])
		if rightChild[cur] > -1:
			if rightChild[cur] in seen:
				return False
			q.append(rightChild[cur])
			seen.add(rightChild[cur])
	
	return len(seen) == n
```

### union-find

We can determine the number of indegrees for each node using a hashmap, and then determine connectedness using [[union-find]].

Note that we can probably handwave away the idea that if we can guarantee the indegree and connectedness property, then we can’t possibly have a cycle.

```python
def validateBinaryTreeNodes(self, n: int, leftChild: List[int], rightChild: List[int]) -> bool:
	indegrees = {node: 0 for node in range(n)}
	uf = UnionFind(n)
	  
	for node in range(n):
		left, right = leftChild[node], rightChild[node]
	  
		if left > -1:
			indegrees[left] += 1
			uf.union(node, left)
	  
		if right > -1:
			indegrees[right] += 1
			uf.union(node, right)
	  
	# requirement 1: one node with indegree == 0
	# and every other node has indegree == 1
	num_roots = 0
	for indegree in indegrees.values():
		if indegree > 1:
			return False
		if indegree == 0:
			num_roots += 1
	valid = num_roots == 1
	  
	# requirement 2: ensure every node is connected
	for node in range(n):
		uf.find(node)
	valid = valid and len(set(uf.parents)) == 1
	  
	return valid
```
