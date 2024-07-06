---
type: leetcode
title: 881. boats to save people
tags:
  - two-pointer
  - sorting
  - greedy
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-19
---

You are given an array `people` where `people[i]` is the weight of the `ith` person, and an **infinite number of boats** where each boat can carry a maximum weight of `limit`. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most `limit`.

Return _the minimum number of boats to carry every given person_.

## solution

The restriction that each boat can hold at most 2 people makes this question not too hard. We realize to put two people in a boat, we want to save the lightest people to go with the heaviest people.

So, if we sort the people and can fit the remaining heaviest and remaining lightest person together, we should, because that lightest person will benefit the heaviest person the most (the next heavier person is guaranteed to work with the lightest person + maybe heavier people). This is the root of the greedy intuition.

```python
def numRescueBoats(self, people: List[int], limit: int) -> int:
	n = len(people)
	people.sort()
	
	ans = 0
	l, r = 0, n-1
	while l <= r:
		if people[l] + people[r] <= limit:
			ans += 1
			l += 1
			r -= 1
		else:
			ans += 1
			r -= 1
	return ans
```
