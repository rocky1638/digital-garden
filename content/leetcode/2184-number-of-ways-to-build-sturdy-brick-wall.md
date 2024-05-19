---
type: leetcode
title: 2184. number of ways to build sturdy brick wall
tags:
  - dfs
  - dp
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-19
---

You are given integers `height` and `width` which specify the dimensions of a brick wall you are building. You are also given a **0-indexed** array of **unique** integers `bricks`, where the `ith` brick has a height of `1` and a width of `bricks[i]`. You have an **infinite** supply of each type of brick and bricks may **not** be rotated.

Each row in the wall must be exactly `width` units long. For the wall to be **sturdy**, adjacent rows in the wall should **not** join bricks at the same location, except at the ends of the wall.

Return _the number of ways to build a **sturdy** wall._ Since the answer may be very large, return it **modulo** `109 + 7`.

## solution

This problem is an absolute monster, but really fun!

First off, we need to figure out all the possible ways that we can build up a wall using the `bricks` that we are given. This is very similar to [[518-coin-change-ii]], and I accomplished this using depth-first search.

```python
def _getPossibleBrickCombos(self, width, bricks):
	combos = []
	acc = []
	s = 0
	  
	def recurse():
		nonlocal combos
		nonlocal acc
		nonlocal s
		  
		if s == width:
			combos.append(acc[:])
		elif s > width:
			return
		  
		else:
			for brick in bricks:
				acc.append(brick)
				s += brick
				recurse()
				s -= brick
				acc.pop()

	recurse()
	return combos
```

Next, we want to think about how to define when two different brick combos are allowed to be adjacent to each other. We know that two brick configurations can be adjacent if they don’t share any seams. As such, let’s first turn all of our brick configurations into a list of seam indices.

```python
def _toBreakpoint(self, brick_combos: list[list[int]]):
	"""
	Convert a list of brick sizes to breakpoint indices.
	  
	E.g. [1,1,1] becomes [1,2]
	"""
	res = []
	for combo in brick_combos:
		bp = set()
		acc = 0
		for val in combo[:-1]:
			bp.add(acc + val)
			acc += val
		res.append(bp)
	return res
```

Now that we have these, we can use a nested for loop to figure out all valid pairs of brick configurations.

```python
def _computeTransitions(self, breakpoints: list[set[int]]):
	transitions = defaultdict(list)
	  
	for i in range(len(breakpoints[:-1])):
		for j in range(i+1, len(breakpoints)):
			# no intersection, will be sturdy beside each other
			if len(breakpoints[i] & breakpoints[j]) == 0:
				transitions[tuple(breakpoints[i])].append(tuple(breakpoints[j]))
				transitions[tuple(breakpoints[j])].append(tuple(breakpoints[i]))
	return transitions
```

Now that we have all the building blocks, we can use dynamic programming to calculate the possible ways we can create a wall of height `h`. Note that the recursive relation is intuitive - the number of ways we can build wall of height $h$ with a certain brick configuration _on top_ is equal to the sum of all the ways we can build walls of height $h-1$ with _valid adjacent configurations._ This is very similar in concept to a simple DP problem like [[45-jump-game-ii]].

Here’s the code that ties it all together.

```python
def buildWall(self, height: int, width: int, bricks: List[int]) -> int:
	possible_brick_combos = self._getPossibleBrickCombos(width, bricks)
	breakpoints = self._toBreakpoint(possible_brick_combos)
	breakpoints_tuple = [tuple(bp) for bp in breakpoints]
	transitions = self._computeTransitions(breakpoints)
	  
	# combos of phone number equiv
	bp_to_idx = {tuple(bp): idx for idx, bp in enumerate(breakpoints)}
	dp = [1] * len(breakpoints)
	  
	for h in range(height-1):
		next_dp = [0] * len(breakpoints)

		for i in range(len(dp)):
			compatible_bps = transitions[breakpoints_tuple[i]]
			compatible_idx = [bp_to_idx[bp] for bp in compatible_bps]
	  
			# EDGE CASE: when brick is single piece,
			# it can stack on top of itself
			if len(breakpoints_tuple[i]) == 0:
			next_dp[i] += dp[i]
	  
			for idx in compatible_idx:
				next_dp[i] += dp[idx]
		dp = [val % (10**9+7) for val in next_dp]
	return sum(dp) % (10**9+7)
```
