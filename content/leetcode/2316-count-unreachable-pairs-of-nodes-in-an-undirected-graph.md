---
type: leetcode
title: 2316. count unreachable pairs of nodes in an  undirected graph
tags:
  - dfs
  - bfs
  - union-find
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-22
---

You are given an integer `n`. There is an **undirected** graph with `n` nodes, numbered from `0` to `n - 1`. You are given a 2D integer array `edges` where `edges[i] = [ai, bi]` denotes that there exists an **undirected** edge connecting nodes `ai` and `bi`.

Return _the **number of pairs** of different nodes that are **unreachable** from each other_.

## solution

Conceptually, this problem is pretty simple. We want to find the size of each disjoint set in our graph, and then multiply the sizes of these sets together (if one set has 3 items and the other has 2, there’s 6 pairs of nodes that are unreachable from each other).

To find disjoint sets, we can use BFS, DFS, or union find. I chose to union find for practice.

Then, the naive approach to finding the number of pairs is to use a nested loop, multiplying each pair of counts together. However, this is $O(n^2)$.

Instead, we can use a sort of “snowball” approach, where we first multiply $A$ and $B$ together. Once this is done, we realize that both $A$ and $B$ will multiply with $C$, so we can add $A$ and $B$ and multiply with $C$, and so on.

```python
def countPairs(self, n: int, edges: List[List[int]]) -> int:
	parents = [i for i in range(n)]
	sizes = [1]*n
	  
	def find(x):
		if x != parents[x]:
			parents[x] = find(parents[x])
		return parents[x]
	  
	def union(u, v):
		pu, pv = find(u), find(v)

		if pu == pv:
			return
	  
		if sizes[pu] > sizes[pv]:
			parents[pv] = pu
			sizes[pu] += sizes[pv]
		else:
			parents[pu] = pv
			sizes[pv] += sizes[pu]
	  
	for u, v in edges:
		union(u, v)
	  
	# run find on every node again to compress paths
	parents = [find(x) for x in parents]
	  
	freqs = [val for key, val in Counter(parents).items()]
	ans = 0
	group_count = freqs[0]
	  
	for i in range(1, len(freqs)):
		ans += freqs[i] * group_count
		group_count += freqs[i]
	return ans
```
