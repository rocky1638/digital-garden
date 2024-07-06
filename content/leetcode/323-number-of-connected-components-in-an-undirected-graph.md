---
type: leetcode
title: 323. number of connected components in an undirected graph
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/
date: 2022-12-22
updated: 2024-06-08
tags:
  - bfs
  - union-find
  - graph
---

You have a graph of `n` nodes. You are given an integer `n` and an array `edges` where `edges[i] = [ai, bi]` indicates that there is an edge between `ai` and `bi` in the graph.

Return _the number of connected components in the graph_.

## solutions

### bfs

We loop through the nodes in the graph, and do standard BFS through the graph from nodes if they are not yet seen.

Everytime we have to initiate a BFS search from an unseen node, we know that that is a connected component, because if was part of another component we would have already seen it in an earlier BFS.

Our runtime is $O(E+V)$, as we only enqueue every node once and check every edge twice.

```python
def countComponents(self, n: int, edges: List[List[int]]) -> int:
	seen = set()
	
	# create graph
	g = defaultdict(list)
	for n1, n2 in edges:
		g[n1].append(n2)
		g[n2].append(n1)
	
	def bfs(node):
		nonlocal g
		nonlocal seen

		q = collections.deque([node])
		while q:
			cur = q.popleft()
			for neighbor in g[cur]:
				if neighbor not in seen:
					q.append(neighbor)
					seen.add(neighbor)
	
	ans = 0
	for node in range(n):
		if node not in seen:
			bfs(node)
			ans += 1

	return ans
```

### union-find

Instead of using a BFS with a visited set, we can use union find through all of the edges to find components, and count the distinct parents afterwards.

The runtime of this, when optimizing for balanced trees in our union find, is $O(n + m\log n)$, but because we use path compression along the way (line 7 in the solution), we can get amortized constant time lookup of node parents, meaning our runtime improves to $O(m+n)$.

```python
def countComponents(self, n: int, edges: List[List[int]]) -> int:
	parents = [i for i in range(n)]
	sizes = [1]*n
	  
	def find(u):
		if u != parents[u]:
			parents[u] = find(parents[u])
		return parents[u]
	  
	def union(u, v):
		pu, pv = find(u), find(v)
		  
		if pu == pv:
			return

		if sizes[pu] < sizes[pv]:
			pu, pv = pv, pu

		parents[pv] = pu
		sizes[pu] += sizes[pv]
	  
	for u, v in edges:
		union(u, v)

	parents = [find(u) for u in parents]
	return len(set(parents))
```
