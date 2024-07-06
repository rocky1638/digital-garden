---
type: leetcode
title: 1136. parallel courses
tags:
  - bfs
  - topological-sort
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-23
---

You are given an integer `n`, which indicates that there are `n` courses labeled from `1` to `n`. You are also given an array `relations` where `relations[i] = [prevCoursei, nextCoursei]`, representing a prerequisite relationship between course `prevCoursei` and course `nextCoursei`: course `prevCoursei` has to be taken before course `nextCoursei`.

In one semester, you can take **any number** of courses as long as you have taken all the prerequisites in the **previous** semester for the courses you are taking.

Return _the **minimum** number of semesters needed to take all courses_. If there is no way to take all the courses, return `-1`.

## solution

We use the ideas of [[topological-sort]] and breadth-first search to solve this problem.

We know that the minimum number of semesters we can take is the length of the longest chain of dependencies (i.e. if A → B → C, we’ll need to take A in semester 1, B in semester 2, C in semester 3).

---

First, we construct a map that counts the indegrees for each node. We know that we can

Essentially, we need to find the depth of the BFS required to visit all nodes, starting with nodes of indegree 0, and only visiting a neighbor node once we’ve already visited all of its prerequisite nodes. We do this by decrementing the indegree of the neighbor node every time we visit a prerequisite node.

```python
def minimumSemesters(self, n: int, relations: List[List[int]]) -> int:
	# find all courses with no prereqs (no indegrees)
	g = defaultdict(list)
	indegrees = Counter()
	  
	for prev, nex in relations:
		g[prev].append(nex)
		indegrees[nex] += 1
	  
	# parallel bfs from all of those courses
	q = deque()
	visited = set()
	for node in range(1, n+1):
		if indegrees[node] == 0:
			q.append(node)
			visited.add(node)
	  
	level = 0
	while q:
		level_len = len(q)
	  
		for i in range(level_len):
			cur = q.popleft()
			  
			for nex in g[cur]:
				indegrees[nex] -= 1
				if nex not in visited and indegrees[nex] == 0:
					q.append(nex)
					visited.add(nex)
		level += 1
  
	return level if len(visited) == n else -1
```
