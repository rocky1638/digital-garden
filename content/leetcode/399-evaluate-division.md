---
type: leetcode
title: 399. evaluate division
tags:
  - bfs
  - graph
  - union-find
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-08
updated: 2024-08-08
---

You are given an array of variable pairs `equations` and an array of real numbers `values`, where `equations[i] = [Ai, Bi]` and `values[i]` represent the equation `Ai / Bi = values[i]`. Each `Ai` or `Bi` is a string that represents a single variable.

You are also given some `queries`, where `queries[j] = [Cj, Dj]` represents the `jth` query where you must find the answer for `Cj / Dj = ?`.

Return _the answers to all queries_. If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

**Note:** The variables that do not occur in the list of equations are undefined, so the answer cannot be determined for them.

## solutions

Here are the key intuitions:

- For each equation, containing $x$ and $y$, we gain information about how to represent $x$ in terms of $y$, and vice versa.
- To solve any query, we just need to get both of the variables in the equation in terms of a shared variable.

### bfs

Following from the intuition above, we can model our variable relationships as a graph, and traverse (BFS/DFS) from one node and then the other, propagating the multiplier as we traverse.

Once we find a shared variable, we can divide the two variables, in terms of the shared variable.

```python
def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
	"""
	try to get each variable in terms of other variables?
	  
	a / b = 2 -> a: 2b, b: 0.5a
	b / c = 3 -> b: 3c, c: 0.33b
	  
	dict[x][y] = x in terms of y
	{
	a: { b: 2 },
	b: { a: 0.5, c: 3 },
	c: { b: 1/3 }
	}
	  
	query: BFS on both variables to find shared value..
	carry multiplier during traversal
	  
	a / c => 2b / .3b = 6
	b / a => 0.5a / a = 0.5
	"""
	  
	d = defaultdict(lambda: {})
	for (x, y), val in zip(equations, values):
		d[x][y] = val
		d[y][x] = 1/val
	  
	def solveQuery(x, y):
		xSeen = {x: 1}
		ySeen = {y: 1}
		  
		# (value, multiplier)
		q = deque([x])

		# construct representations relative to x
		while q:
			val = q.popleft()
		  
			for neighbor, nWeight in d[val].items():
				if neighbor not in xSeen:
					xSeen[neighbor] = xSeen[val] * nWeight
					q.append(neighbor)

		# representations relative to y
		q = deque([y])
		while q:
			val = q.popleft()
		  
			if val in xSeen:
				return xSeen[val] / ySeen[val]

			for neighbor, nWeight in d[val].items():
				if neighbor not in ySeen:
					ySeen[neighbor] = ySeen[val] * nWeight
					q.append(neighbor)

		return -1.0

	ans = []
	for x, y in queries:
		if not (x in d and y in d):
			ans.append(-1.0)
			continue
		ans.append(solveQuery(x, y))
	return ans
```

### modified union-find

If you think really hard, you can see that we can only return the value of a query if the two variables belong to the same component within the graph.

Furthermore, if we’re path shortening and keeping track of the “root” of each component (as well as the multiplier between the node and the parent), we can divide the two multipliers of the two variables in constant time.

The difficulty comes in trying to modify the union find algorithm to add stored weights.
