---
type: leetcode
title: 1443. minimum time to collect all apples in a tree
tags:
  - dfs
  - tree
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-02
updated: 2024-09-02
---

Given an undirected tree consisting of `n` vertices numbered from `0` to `n-1`, which has some apples in their vertices. You spend 1 second to walk over one edge of the tree. _Return the minimum time in seconds you have to spend to collect all apples in the tree, starting at **vertex 0** and coming back to this vertex._

The edges of the undirected tree are given in the array `edges`, where `edges[i] = [ai, bi]` means that exists an edge connecting the vertices `ai` and `bi`. Additionally, there is a boolean array `hasApple`, where `hasApple[i] = true` means that vertex `i` has an apple; otherwise, it does not have any apple.

## solution

Logically, we always collect all the apples in the subtree before returning to the parent, for the shortest path.

With DFS, we can do this, and realize that if the subtree had apples to collect, then we take the total steps for the subtree, and add 2.

As a minor optimization, we can just keep a `parent` reference in our recursive call to avoid having to use a `seen` set.

```python
def minTime(self, n: int, edges: List[List[int]], hasApple: List[bool]) -> int:
	"""
	time to collect all apples in tree:
	  
	time to collect in node.child + 2
	if collected apples = 0, this whole value is 0
	(because we didn't need to go down the child subtree)
	"""
	  
	tree = defaultdict(list)
	for u1, u2 in edges:
		tree[u1].append(u2)
		tree[u2].append(u1)
	  
	seen = set([0])
	  
	def recurse(node):
		total_steps, root_collected = 0, False
	  
		for neighbor in tree[node]:
			if neighbor not in seen:
				seen.add(neighbor)
				steps, collected = recurse(neighbor)
				if collected:
					total_steps += steps + 2
					root_collected = True
	  
		return total_steps, root_collected or hasApple[node]
	  
	return recurse(0)[0]
```
