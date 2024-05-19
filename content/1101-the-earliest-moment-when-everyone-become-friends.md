---
type: leetcode
title: "1101. the earliest moment when everyone become friends"
tags:
  - union-find
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-19
---

There are n people in a social group labeled from `0` to `n - 1`. You are given an array `logs` where `logs[i] = [timestampi, xi, yi]` indicates that `xi` and `yi` will be friends at the time `timestampi`.

Friendship is **symmetric**. That means if `a` is friends with `b`, then `b` is friends with `a`. Also, person `a` is acquainted with a person `b` if `a` is friends with `b`, or `a` is a friend of someone acquainted with `b`.

Return _the earliest time for which every person became acquainted with every other person_. If there is no such earliest time, return `-1`.

## solution

At first, I was thinking about a solution where we would construct a graph/adjacency list of friendships, and after adding each edge, run DFS from a random friend to see if we could reach every other friend.

However, this would have a runtime of $O(tn^2)$, as for each timestamp, we would conduct a DFS on the graph of $n$ nodes, which would have at most $n+(n-1)+(n-2)\dots+1$ connections, which is approximately equivalent to $n^2$.

---

Instead, the realization required here is that we are explictly dealing with the joining of disjoint components/sets, and want to return whenever we realize we only have one large graph component remaining (i.e. when every friend is in the same connected set).

This is the perfect use case for [[union-find]], and basically just uses union find verbatim, after sorting the logs.

```python
def earliestAcq(self, logs: List[List[int]], n: int) -> int:
	# initialize union find
	parents = [i for i in range(n)]
	sizes = [1] * n
	  
	def find(u):
		# path compression (parents always shows root)
		if u != parents[u]:
			parents[u] = find(parents[u])
		return parents[u]
	  
	def union(u, v):
		pu, pv = find(u), find(v)
		  
		if pu == pv:
			return False
		  
		# ensure u is bigger
		if sizes[pu] < sizes[pv]:
			u, v = v, u

		parents[pv] = pu
		sizes[u] += sizes[v]
		return True
	  
	  
	logs.sort(key=lambda x: x[0])
	for timestamp, u, v in logs:
		union(u, v)

		if len(set([find(p) for p in parents])) == 1:
			return timestamp
	  
	return -1
```

Above, I do a slightly weird $O(n)$ check within the loop to determine our end condition, but we can just keep a counter tracking number of distinct groups, reducing that value by 1 whenever we successfully perform a `union`.

```python
def earliestAcq(self, logs: List[List[int]], n: int) -> int:
	# initialize union find
	parents = [i for i in range(n)]
	sizes = [1] * n
	groups = n
	  
	def find(u):
		# path compression (parents always shows root)
		if u != parents[u]:
			parents[u] = find(parents[u])
		return parents[u]
	  
	def union(u, v):
		nonlocal groups
		pu, pv = find(u), find(v)
		  
		if pu == pv:
			return False
		  
		# ensure u is bigger
		if sizes[pu] < sizes[pv]:
			u, v = v, u

		parents[pv] = pu
		sizes[u] += sizes[v]
		return True
	  
	  
	logs.sort(key=lambda x: x[0])
	for timestamp, u, v in logs:
		union(u, v)

		if groups == 1:
			return timestamp
	  
	return -1
```
