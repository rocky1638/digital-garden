---
type: leetcode
title: 1584. min cost to connect all points
tags:
  - union-find
  - sorting
  - graph
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-02
---

You are given an array `points` representing integer coordinates of some points on a 2D-plane, where `points[i] = [xi, yi]`.

The cost of connecting two points `[xi, yi]` and `[xj, yj]` is the **manhattan distance** between them: `|xi - xj| + |yi - yj|`, where `|val|` denotes the absolute value of `val`.

Return _the minimum cost to make all points connected._ All points are connected if there is **exactly one** simple path between any two points.

## solution

Here, we are essentially trying to find the minimum spanning tree (MST) of the graph.

We use Kruskal’s MST algorithm below, implemented with union find to determine which edges can be skipped in amortized constant time.

1. We enumerate all possible edges and costs, and sort them by cost.
2. Going through costs from small to large, we connect two points if they are not yet part of the same connected tree.

```python
def minCostConnectPoints(self, points: List[List[int]]) -> int:
	n = len(points)
	edges = []
	point_to_idx = {
		(x,y): i
		for i, (x, y) in enumerate(points)
	}
	  
	for i in range(n-1):
		for j in range(i+1, n):
			x1, y1 = points[i]
			x2, y2 = points[j]
			cost = abs(x1-x2) + abs(y1-y2)
			edges.append((cost, x1, y1, x2, y2))
	edges.sort()
	  
	# start with disconnected points
	parents = [tuple(points[idx]) for idx in range(n)]
	# size of tree rooted at point i
	sizes = [1]*n
	  
	def union(u, v):
		pu, pv = find(u), find(v)
		# already unioned, skip edge
		if pu == pv:
			return False
	  
		pui, pvi = point_to_idx[pu], point_to_idx[pv]
		if sizes[pui] < sizes[pvi]:
			pu, pv = pv, pu
			pui, pvi = pvi, pui

		parents[pvi] = pu
		sizes[pui] += sizes[pvi]
		return True

	def find(u):
		ui = point_to_idx[u]
		if u != parents[ui]:
			parents[ui] = find(parents[ui])
		return parents[ui]

	ans = 0
	for cost, x1, y1, x2, y2 in edges:
		if union((x1, y1), (x2, y2)):
			ans += cost
	return ans
```
