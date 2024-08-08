---
type: leetcode
title: 473. matchsticks to square
tags:
  - dfs
  - backtracking
  - memoization
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-14
updated: 2024-07-14
---

You are given an integer array `matchsticks` where `matchsticks[i]` is the length of the `ith` matchstick. You want to use **all the matchsticks** to make one square. You **should not break** any stick, but you can link them up, and each matchstick must be used **exactly one time**.

Return `true` if you can make this square and `false` otherwise.

## solutions

### backtracking with memoization

We can try to place the current matchstick at `idx` into any of the four sides that still have room for it. In this way, we can parametrize all four of the sides and then memoize the calls.

```python
def makesquare(self, matchsticks: List[int]) -> bool:
	s = sum(matchsticks)
	n = len(matchsticks)
	  
	# the largest values have the least options in terms
	# of placement, so by sorting in reverse, we reduce the
	# search space from the top
	matchsticks.sort(reverse=True)

	if s % 4 != 0:
	return False
	  
	side_length = s // 4
	  
	@lru_cache
	def recurse(idx, s1, s2, s3, s4):
		sides = [s1, s2, s3, s4]
		  
		if idx == n:
			return len(set(sides)) == 1

		ans = False
		for i in range(4):
			if matchsticks[idx] + sides[i] <= side_length:
				sides[i] += matchsticks[idx]
				ans = ans or recurse(idx+1, *sides)
				sides[i] -= matchsticks[idx]
		return ans
	  
	return recurse(0, 0,0,0,0)
```

### backtracking (greedily filling earliest side)

Instead of parametrizing all of the sides, we can just fill in the sides in order, and 

```python
def makesquare(self, matchsticks: List[int]) -> bool:
	s = sum(matchsticks)
	n = len(matchsticks)
	  
	# the largest values have the least options in terms
	# of placement, so by sorting in reverse, we reduce the
	# search space from the top
	matchsticks.sort(reverse=True)
	if s % 4 != 0:
		return False
	  
	side_length = s // 4
	sides = [0]*4
	  
	def recurse(idx):
		if idx == n:
			return len(set(sides)) == 1

		for i in range(4):
			if matchsticks[idx] + sides[i] <= side_length:
				sides[i] += matchsticks[idx]
				if recurse(idx+1):
					return True
				sides[i] -= matchsticks[idx]
		  
				if sides[i] == 0:
					break
		return False
	  
	return recurse(0)
```
