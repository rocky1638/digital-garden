---
type: leetcode
title: 1462. course schedule iv
tags:
  - topological-sort
  - dfs
  - memoization
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-24
updated: 2024-08-24
---

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `ai` first if you want to take course `bi`.

- For example, the pair `[0, 1]` indicates that you have to take course `0` before you can take course `1`.

Prerequisites can also be **indirect**. If course `a` is a prerequisite of course `b`, and course `b` is a prerequisite of course `c`, then course `a` is a prerequisite of course `c`.

You are also given an array `queries` where `queries[j] = [uj, vj]`. For the `jth` query, you should answer whether course `uj` is a prerequisite of course `vj` or not.

Return _a boolean array_ `answer`_, where_ `answer[j]` _is the answer to the_ `jth` _query._

## solutions

### dfs w/ memoization

For each query, just try to DFS from `src` to `target` using the DAG created by the prerequisites.

```python
def checkIfPrerequisite(self, numCourses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
	# construct graph
	g = defaultdict(list)
	  
	for u, v in prerequisites:
		g[u].append(v)
	  
	memo = {}
	def dfs(src, target):
		if (src, target) in memo:
			return memo[(src, target)]
	  
		if src == target:
			return True

		reachable = False
		for neighbor in g[src]:
			reachable = reachable or dfs(neighbor, target)
	  
		memo[(src, target)] = reachable
		return reachable
	  
	res = []
	for src, target in queries:
		res.append(dfs(src, target))
	return res
```

### construct prerequisite set per node with topological sort

Instead of running the graph traversal for every query, we can instead try to construct a mapping from a node to its prerequisites, which will allow us to answer every query in constant time.

We can do this by running BFS, and adding `cur`, as well as `cur`’s prerequisites, to the prerequisites set of `neighbor`.

Because we run our BFS using a topological sort method, we know that we’re encountering nodes starting with the ones that have no prerequisites, and so we can be sure that every node’s prerequisite set is complete.

```python
def checkIfPrerequisite(self, numCourses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
	# construct graph
	g = defaultdict(list)
	indegrees = defaultdict(int)
	node_to_prereqs = defaultdict(set)
	  
	for u, v in prerequisites:
		g[u].append(v)
		indegrees[v] += 1

	q = deque()
	for node in range(numCourses):
		if indegrees[node] == 0:
			q.append(node)
	  
	while q:
		cur = q.popleft()
	  
		for neighbor in g[cur]:
			# add cur and cur's prereqs to neighbor prereqs
			node_to_prereqs[neighbor].add(cur)
			node_to_prereqs[neighbor].update(node_to_prereqs[cur])
	  
			indegrees[neighbor] -= 1
			if indegrees[neighbor] == 0:
				q.append(neighbor)

	res = []
	for src, target in queries:
		res.append(src in node_to_prereqs[target])
	return res
```
