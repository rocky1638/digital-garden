---
type: leetcode
title: 825. friends of appropriate ages
tags:
  - binary-search
  - math
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-31
updated: 2024-08-31
---

There are `n` persons on a social media website. You are given an integer array `ages` where `ages[i]` is the age of the `ith` person.

A Person `x` will not send a friend request to a person `y` (`x != y`) if any of the following conditions is true:

- `age[y] <= 0.5 * age[x] + 7`
- `age[y] > age[x]`
- `age[y] > 100 && age[x] < 100`

Otherwise, `x` will send a friend request to `y`.

Note that if `x` sends a request to `y`, `y` will not necessarily send a request to `x`. Also, a person will not send a friend request to themself.

Return _the total number of friend requests made_.

## solutions

### math + binary search

```python
def numFriendRequests(self, ages: List[int]) -> int:
	res = 0
	ages.sort()
	for i, x in enumerate(ages):
		# acceptable range: (0.5x+7, x]
		min_age, max_age = x*0.5+7, x
		  
		# we DON'T want to include people with min_age
		l = bisect.bisect_right(ages, min_age)
		# we want to include all people same age as x
		r = bisect.bisect_right(ages, max_age)
		  
		# l is on first valid value on right
		# r is on the index to the right of the last valid value
		# so, number of valid values in the range is r-l
		# then, subtract 1 because x will always be in this range
		res += max(0,r-l-1)
	return res
```

### buckets + nested loop

```python
def numFriendRequests(self, ages: List[int]) -> int:
	freqs = [0]*121
	for age in ages:
		freqs[age] += 1

	res = 0
	for x, cntX in enumerate(freqs):
		for y, cntY in enumerate(freqs):
			if y > x: continue
			if y <= 0.5*x+7: continue
	  
			# everyone age X sends request to everyone age Y
			res += cntX * cntY
	  
			# if X == Y, then we have to remove X instances of
			# friends in X sending requests to themselves
			if x == y: res -= cntX
	return res
```

### frequency prefix sum

TODO
