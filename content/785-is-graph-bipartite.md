---
type: leetcode
title: 785. is graph bipartite?
tags:
  - dfs
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-05
updated: 2024-10-05
---

There is an **undirected** graph with `n` nodes, where each node is numbered between `0` and `n - 1`. You are given a 2D array `graph`, where `graph[u]` is an array of nodes that node `u` is adjacent to. More formally, for each `v` in `graph[u]`, there is an undirected edge between node `u` and node `v`. The graph has the following properties:

- There are no self-edges (`graph[u]` does not contain `u`).
- There are no parallel edges (`graph[u]` does not contain duplicate values).
- If `v` is in `graph[u]`, then `u` is in `graph[v]` (the graph is undirected).
- The graph may not be connected, meaning there may be two nodes `u` and `v` such that there is no path between them.

A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that **every** edge in the graph connects a node in set `A` and a node in set `B`.

Return `true` _if and only if it is **bipartite**_.

## solutions

### bfs coloring

```python
def isBipartite(self, graph: List[List[int]]) -> bool:
	colors = {}
	  
	def bfs(node):
		q = deque([node])
		color = 0
	  
		while q:
			level_len = len(q)
	  
			for _ in range(level_len):
				x = q.popleft()
				colors[x] = color
	  
				for neighbor in graph[x]:
					if neighbor in colors:
						if colors[neighbor] == color:
							return False
					else:
						q.append(neighbor)
			color ^= 1

		return True

	for node in range(len(graph)):
		if node not in colors:
			if not bfs(node):
				return False
	  
	return True
```

### dfs coloring
