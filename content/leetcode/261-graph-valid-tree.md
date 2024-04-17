---
title: "261. graph valid tree"
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/graph-valid-tree/
date: 2022-12-13
updated: 2024-03-29
tags:
  - graph
---

You have a graph of `n` nodes labeled from `0` to `n - 1`. You are given an integer n and a list of `edges` where `edges[i] = [ai, bi]` indicates that there is an undirected edge between nodes `ai` and `bi` in the graph.

Return `true` _if the edges of the given graph make up a valid tree, and_ `false` _otherwise_.

## solutions

A tree is defined as a graph that has no cycles, and contains a path that allows you to reach every node in the graph.

We can just DFS or BFS starting from the first node, and keep track of the nodes that we’ve seen.

### dfs

Because the graph is bidirectional, we keep track of what the parent node is in each recursive call, so we don’t detect trivial cycles. Then, at the end, if we never see a node that we’ve already seen, and we have visited every node, then we know that our graph is a valid tree.

```python
def validTree(self, n: int, edges: List[List[int]]) -> bool:
	g = collections.defaultdict(list)

	for a, b in edges:
		g[a].append(b)
		g[b].append(a)
	
	seen = set()

	def recurse(node, parent):
		for neighbor in g[node]:
			if neighbor == parent:
				continue
			if neighbor in seen:
				return False
		
			seen.add(neighbor)

			if not recurse(neighbor, node):
				return False

		return True
	
	seen.add(0)
	return recurse(0, -1) and len(seen) == n
```

### bfs

Similar idea for the BFS. I ended up keeping track of the edges that we’ve already used to filter out “fake” cycles where we could revisit a node by reusing an edge.

```python
def validTree(self, n: int, edges: List[List[int]]) -> bool:
	g = defaultdict(list)
	  
	for u1, u2 in edges:
		g[u1].append(u2)
		g[u2].append(u1)

	# set of edges (u1, u2) that we've already used
	seen = set()
	# to make sure we visit all the nodes
	seen_nodes = set([0])

	q = deque([0])
	  
	while q:
		cur = q.pop()
	  
		for neighbor in g[cur]:
			if (cur, neighbor) in seen:
				continue
	  
			# cycle
			if neighbor in seen_nodes:
				return False
	  
			seen.add((cur, neighbor))
			seen.add((neighbor, cur))
			seen_nodes.add(neighbor)
			  
			q.appendleft(neighbor)

	return len(seen_nodes) == n
```
