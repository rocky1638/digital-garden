---
type: leetcode
title: 2508. add edges to make degrees of all nodes even
tags:
  - graph
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-06
updated: 2024-08-06
---

There is an **undirected** graph consisting of `n` nodes numbered from `1` to `n`. You are given the integer `n` and a **2D** array `edges` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi`. The graph can be disconnected.

You can add **at most** two additional edges (possibly none) to this graph so that there are no repeated edges and no self-loops.

Return `true` _if it is possible to make the degree of each node in the graph even, otherwise return_ `false`_._

The degree of a node is the number of edges connected to it.

## solution

There’s a couple of revelations to make here, but it is pretty “hard-coded” in the grand scheme of things.

1. We realize that by adding an edge, we increase the degree of two nodes by 1.
	- Thus, with 2 edges, we can at most make 4 nodes from odd to even.
2. When we add an edge, we change the polarity of two nodes. Therefore, if we start with an odd number of odd nodes, it’s impossible to reach a valid solution.
3. Therefore, the only starting states worth checking are when there are 0, 2, or 4 odd nodes.
	- For each of these, just logic your way through it.

```python
def isPossible(self, n: int, edges: List[List[int]]) -> bool:
	degrees = {u: 0 for u in range(1, n+1)}
	g = defaultdict(set)
	for u1, u2 in edges:
		degrees[u1] += 1
		degrees[u2] += 1
		g[u1].add(u2)
		g[u2].add(u1)
	  
	odds = []
	for i in range(1, n+1):
		if degrees[i] & 1:
			odds.append(i)
	  
	# an edge changes the degrees of two nodes,
	# so if we have 1 or 3 odd nodes, it's impossible
	# to get rid of all the odds.
	if len(odds) not in {0, 2, 4}:
		return False

	# already a valid solution
	if len(odds) == 0:
		return True

	if len(odds) == 2:
		u1, u2 = odds
		# if edge already exists, there needs to be an even
		# node that isn't yet connected to either odd one
		if u2 in g[u1]:
			for node in range(1, n+1):
				if node != u1 and node != u2:
					if u1 not in g[node] and u2 not in g[node]:
						return True
			return False
	  
		# if edge doesn't already exist, just connect them
		else:
			return True
	  
	if len(odds) == 4:
		# we need to use each of our edges to
		# make two odd nodes even.
		  
		# just need to have two available edges,
		# one between a/b and one between c/d
		  
		u1, u2, u3, u4 = odds
		avail_for_u1 = {u2, u3, u4} - g[u1]
		  
		# if u1 is already connected to
		# the other three, then impossible
		if not avail_for_u1:
			return False
		  
		# if not, for each node u1 can connect to,
		# check if the other two can connect.
		# if any of those combinations work, return True.
		is_valid = False
		for node in avail_for_u1:
			if node == u2:
				is_valid = is_valid or u4 not in g[u3]
			if node == u3:
				is_valid = is_valid or u4 not in g[u2]
			if node == u4:
				is_valid = is_valid or u3 not in g[u2]
		return is_valid
```

Here’s a slightly more succinct from the legend `lee215`.

```python
def isPossible(self, n, edges):
	G = [set() for i in range(n)]
	for i,j in edges:
		G[i-1].add(j-1)
		G[j-1].add(i-1)

	odd = [i for i in range(n) if len(G[i]) % 2]
	
	def f(a,b):
		return a not in G[b]
	
	if len(odd) == 2:
		a, b = odd
		return any(f(a,i) and f(b,i) for i in range(n))
	
	if len(odd) == 4:
		a,b,c,d = odd
		return f(a,b) and f(c,d) or \
				f(a,c) and f(b,d) or \
				f(a,d) and f(c,b)
	return len(odd) == 0
```
