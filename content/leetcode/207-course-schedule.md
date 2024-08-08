---
title: 207. course schedule
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/course-schedule/
date: 2022-11-20
updated: 2024-08-05
tags:
  - topological-sort
  - graph
  - bfs
children:
  - "[[210-course-schedule-ii]]"
---

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

## solution

This is a standard topological sort. A prerequisite course has a directed edge towards the course that requires it.

```python
def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
	g = defaultdict(list)
	ind = Counter()
	
	for a, b in prerequisites:
		# create graph adjacency list
		g[a].append(b)
		# count indegrees for each node
		ind[b] += 1
	
	# push all nodes with indegree 0 into a queue
	q = deque()
	topsort = []
	for node in range(numCourses):
		if ind[node] == 0:
		q.append(node)
	
	# do bfs, but only push new nodes that have
	#   an indegree of 0 (all prereqs met)
	# decrement indegree as you go
	while q:
		cur = q.popleft()
		topsort.append(cur)
		for neighbor in g[cur]:
			ind[neighbor] -= 1
			if ind[neighbor] == 0:
				q.append(neighbor)
	
	return len(topsort) == numCourses
```
