---
type: leetcode
title: 815. bus routes
tags:
  - graph
  - bfs
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-31
updated: 2024-07-31
---

## solutions

You are given an array `routes` representing bus routes where `routes[i]` is a bus route that the `ith` bus repeats forever.

- For example, if `routes[0] = [1, 5, 7]`, this means that the `0th` bus travels in the sequence `1 -> 5 -> 7 -> 1 -> 5 -> 7 -> 1 -> ...` forever.

You will start at the bus stop `source` (You are not on any bus initially), and you want to go to the bus stop `target`. You can travel between bus stops by buses only.

Return _the least number of buses you must take to travel from_ `source` _to_ `target`. Return `-1` if it is not possible.

### bfs on bus stops w/ nested route traversal

My intuition here is that for finding the shortest path, we want to use some variation of BFS at the root of the problem. Here’s the steps I took when thinking about the question:

1. Construct an adjacency list to represent the bus routes as a directed graph.
	- In order to calculate the “depth" of the traversal in terms of bus routes and not just edges traversed, we need to know which route each edge belongs to.
2. Perform a BFS. For each stop, traverse down all the bus routes that we haven’t traversed yet, adding them to the queue, while keeping track of depth.

Unfortunately, this times out due to the fact that we may need to traverse stops that we’ve already traversed in `traverse_route`, as we can’t stop early as we might need to traverse over a node we’ve already seen to reach an optimal answer??

```python
def numBusesToDestination(self, routes: List[List[int]], source: int, target: int) -> int:
	# construct graph with labeled edges #
	  
	# g[u] = { route_id: v, route_id: v2 }
	route_id = 0
	g = defaultdict(lambda: defaultdict(int))
	for route in routes:
		for i in range(len(route)):
			if i+1 == len(route):
				next_node = route[0]
			else:
				next_node = route[i+1]
	  
			g[route[i]][route_id] = next_node
		route_id += 1

	routes_used = set()
	seen_depths = {}
	  
	def traverse_route(node, route_id):
		new_nodes = []
		cur = g[node][route_id]
		while cur != node:
			if cur not in seen_depths:
				new_nodes.append(cur)
				seen_depths[cur] = seen_depths[node]
			cur = g[cur][route_id]
		return new_nodes
	  
	q = deque([source])
	depth = 0
	while q:
		level_len = len(q)
		  
		for _ in range(level_len):
			cur = q.popleft()
			seen_depths[cur] = depth
		  
			if cur == target:
				return seen_depths[cur]
		  
			for route_id in g[cur]:
				if route_id not in routes_used:
					new_nodes = traverse_route(cur, route_id)
					q.extend(new_nodes)
		depth += 1
	  
	return -1
```

### bfs on bus routes

The intuition here is that if we’re looking for the shortest path in terms of bus routes, we should BFS on bus routes, as opposed to bus stops.

Following this thinking, we instead construct our graph differently, mapping bus stops to all of the _routes_ that they are a part of.

With this in place, we can initialize our queue with all of the bus routes that `source` belongs to. Then, we BFS. For each bus route, we iterate through every stop in the route, enqueueing any new bus routes that these stops connect to.

At any point, if we happen upon `target`, we know we’ve found the shortest path, because our BFS is proceeding in depth-order through bus routes.

**Notes:**
1. Just like above, we only ever traverse each bus route once.
2. An interesting point is that we should mark a bus route as seen when we **enqueue** and not when we **dequeue**, because we might process duplicate routes within the for-loop on 29 if we don’t do this.

```python
def numBusesToDestination(self, routes: List[List[int]], source: int, target: int) -> int:
	if source == target:
		return 0

	# g[stop] = list(route_ids)
	g = defaultdict(list)
	for i, route in enumerate(routes):
		for j in range(len(route)):
			g[route[j]].append(i)

	routes_used = set()
	  
	# queue of routes
	q = deque(g[source])
	for stop in g[source]:
		routes_used.add(stop)
	  
	depth = 1
	while q:
		level_len = len(q)
	  
		for _ in range(level_len):
			cur = q.popleft()
	  
			for stop in routes[cur]:
				if stop == target:
					return depth
	  
				for connecting_route in g[stop]:
					if connecting_route not in routes_used:
						# do this on queue push and not pop
						# doing it on queue pop causes timeout
						routes_used.add(connecting_route)
						q.append(connecting_route)
		depth += 1
	return -1
