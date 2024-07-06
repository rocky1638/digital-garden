---
type: leetcode
title: 1557. minimum number of vertices to reach all nodes
tags:
  - graph
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-30
---

Given a **directed acyclic graph**, with `n` vertices numbered from `0` to `n-1`, and an array `edges` where `edges[i] = [fromi, toi]` represents a directed edge from node `fromi` to node `toi`.

Find _the smallest set of vertices from which all nodes in the graph are reachable_. It's guaranteed that a unique solution exists.

Notice that you can return the vertices in any order.

## solution

The key and only intuition to reach here is that all we need to do is to find all of the nodes with no incoming edges, or an indegree of zero.

This is because there’s no way we can reach any nodes with no incoming edges unless we start with them. Furthermore, if we assume that all nodes are reachable, then we know that there’s an incoming edge for all the other nodes so they will be reached eventually.

```python
def findSmallestSetOfVertices(self, n: int, edges: List[List[int]]) -> List[int]:
	g = defaultdict(list)
	indegrees = {u: 0 for u in range(n)}
	  
	for u1, u2 in edges:
		g[u1].append(u2)
		indegrees[u2] += 1

	ans = []
	for node in indegrees:
		if indegrees[node] == 0:
			ans.append(node)
	return ans
```
