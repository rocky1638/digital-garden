---
type: leetcode
title: 365. water and jug problem
tags:
  - bfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-25
---

You are given two jugs with capacities `x` liters and `y` liters. You have an infinite water supply. Return whether the total amount of water in both jugs may reach `target` using the following operations:

- Fill either jug completely with water.
- Completely empty either jug.
- Pour water from one jug into another until the receiving jug is full, or the transferring jug is empty.

## solutions

### bfs

We can figure out the various ways we can progress from any state, keeping track of visited states.

```python
def canMeasureWater(self, x: int, y: int, target: int) -> bool:
	def neighbors(a, b):
		res = []
		# Fill jug A
		res.append((x, b))
		# Fill jug B
		res.append((a, y))
		# Empty jug A
		res.append((0, b))
		# Empty jug B
		res.append((a, 0))
		  
		# A into B
		amount_to_pour = min(a, y-b)
		if amount_to_pour > 0:
			res.append((a-amount_to_pour, b+amount_to_pour))
		  
		# B into A
		amount_to_pour = min(b, x-a)
		if amount_to_pour > 0:
			res.append((a+amount_to_pour, b-amount_to_pour))
	  
	return res

	seen = set([(0, 0)])
	q = deque([(0, 0)])
	while q:
		a, b = q.popleft()
		if a + b == target:
			return True
	  
		for ne in neighbors(a, b):
			if ne not in seen:
				seen.add(ne)
				q.append(ne)

	return False
```

### gcd

There is a mathematical proof that can show that all multiples of the GCD of `x` and `y` are achievable, but I don’t like that as a solution to a coding interview.
