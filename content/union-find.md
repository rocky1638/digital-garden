---
type: concept
aliases: 
date: 2023-01-13
updated: 2024-05-19
tags:
  - union-find
---

Union find is a data structure that supports two main functions:
1. `uf.find(u)`, which outputs a unique id so that two nodes have the same id if and only if they are in the same connected component.
2. `uf.union(u, v)`, which connects the components with id `find(u)` and `find(v)` together. If it already connected then return False, else return True.

## example implementation

```python
class UnionFind:
	def __init__(self, n):
		# initialize each node's parent as itself
		self.parent = [i for i in range(n)]
		# store size of each set with i'th node as parent
		self.size = [1] * n
	
	"""
	returns the parent of the set that x belongs to.
	essentially, parent of the set is used to "key"
	the set that it manages.
	"""
	def find(self, x):
		# if x is already a child to smth else, do collapsing find
		if x != self.parent[x]:
			# recursively updates and caches
			self.parent[x] = self.find(self.parent[x]) # Path compression
		return self.parent[x]
	
	def union(self, u, v):
		# find parents of both nodes
		pu, pv = self.find(u), self.find(v)
		if pu == pv: return False  # Return False if u and v are already union
		
		# the larger set becomes the main parent
		if self.size[pu] > self.size[pv]: # Union by larger size
			self.size[pu] += self.size[pv]
			self.parent[pv] = pu
		else:
			self.size[pv] += self.size[pu]
			self.parent[pu] = pv
		return True
```

## video notes

<iframe width="560" height="315" src="https://www.youtube.com/embed/wU6udHRIkcc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

- [01:40](https://www.youtube.com/watch?v=wU6udHRIkcc&t=97s#t=100.70006405912781) introduction to disjoint sets.
	- the intersection of two sets is empty.
- [02:27](https://www.youtube.com/watch?v=wU6udHRIkcc&t=97s#t=147.03424511634827) introduction to `find`.
	- an operation to find which set a value belongs to.
- [03:02](https://www.youtube.com/watch?v=wU6udHRIkcc&t=97s#t=182.87704098283388) `union` operation.
	- we add an edge between two values.
	- we first `find` which set each of the two values belong to.
		- if the two values belong to *different* sets, we can connect them and unionize the two sets.
- [04:34](https://www.youtube.com/watch?v=wU6udHRIkcc&t=97s#t=274.14057215449526) why perform `union`?
	- if we try to add an edge to two values that are already in the same set, then *we will form a cycle if we add that edge.*
- [05:45](https://www.youtube.com/watch?v=wU6udHRIkcc&t=97s#t=345.796532082016) cycle detection with union-find walkthrough.
	- in an algorithm, start with the assumption that each value is in it’s own disjoint set.
- [11:32](https://www.youtube.com/watch?v=wU6udHRIkcc&t=97s#t=692.1407119008179) another walkthrough, graphically.
	- how we actually represent the subgraph components, thinking about parent and children nodes.
	- when we union, we can select **either** parent as the main parent, and set the other parent as the child of the main parent.
		- however, when the two sets have a *different number of nodes*, we should choose the parent of the bigger set to the be the main parent.
- [16:09](https://www.youtube.com/watch?v=wU6udHRIkcc&t=97s#t=969.6093900476837) algorithmic representation example.
	- representing parents in an array/hashmap.
- [24:01](https://www.youtube.com/watch?v=wU6udHRIkcc&t=97s#t=1441.8985860267028) optimizing by collapsing finds.

## references

- https://en.wikipedia.org/wiki/Disjoint-set_data_structure
- https://www.youtube.com/watch?v=wU6udHRIkcc
