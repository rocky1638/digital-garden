---
created_at: 2023-01-17
title: 742. network delay time
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/network-delay-time/
date: 2023-01-17
updated: 2024-05-29
tags:
  - graph
  - djikstra
  - heap
---

You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source node, `vi` is the target node, and `wi` is the time it takes for a signal to travel from source to target.

We will send a signal from a given node `k`. Return _the **minimum** time it takes for all the_ `n` _nodes to receive the signal_. If it is impossible for all the `n` nodes to receive the signal, return `-1`.

## solution

This problem is exactly the single-source-shortest-path (SSSP) problem, and can be solved with Djikstra’s algorithm or the Bellman-Ford algorithm.

```python
def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
	g = defaultdict(list)
	for u, v, cost in times:
		g[u].append((cost, v))
	  
	dists = [inf]*n
	dists[k-1] = 0
	pq = [(0, k)]
	while pq:
		cur_cost, cur_node = heappop(pq)
		for cost, neighbor in g[cur_node]:
			total_cost = cur_cost + cost
			if total_cost < dists[neighbor-1]:
				heappush(pq, (total_cost, neighbor))
				dists[neighbor-1] = total_cost

	ans = 0
	for i in range(len(dists)):
		if dists[i] == inf:
			return -1
		ans = max(ans, dists[i])
	return ans
```

## references

- https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm.
- https://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm.
