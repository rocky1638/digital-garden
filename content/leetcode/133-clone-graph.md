---
type: leetcode
title: 133. clone graph
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/clone-graph/
date: 2022-11-19
updated: 2024-08-23
tags:
  - hashmap
  - bfs
  - graph
---

Given a reference of a node in a **[connected](https://en.wikipedia.org/wiki/Connectivity_(graph_theory)#Connected_graph)** undirected graph.

Return a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) (clone) of the graph.

## solution

We can BFS, making sure to traverse each node only once. Whenever we pop a node, we add all of its neighbors to `node.neighbors`, creating new cloned nodes and adding them to our mapping dictionary if necessary. If the node has not yet been processed, enqueue it.

```python
def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
	if not node:
		return None
	  
	d = {node: Node(node.val)}
	q = deque([node])
	  
	while q:
		cur = q.popleft()
	  
		for neighbor in cur.neighbors:
			# only visit each node once
			if neighbor not in d:
				new_neighbor = Node(neighbor.val)
				d[neighbor] = new_neighbor
				q.append(neighbor)

			# store all neighbor relationships
			d[cur].neighbors.append(d[neighbor])
	  
	return d[node]
```
