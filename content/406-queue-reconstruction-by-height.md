---
type: leetcode
title: 406. queue reconstruction by height
tags:
  - sorting
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-09-06
---

You are given an array of people, `people`, which are the attributes of some people in a queue (not necessarily in order). Each `people[i] = [hi, ki]` represents the `ith` person of height `hi` with **exactly** `ki` other people in front who have a height greater than or equal to `hi`.

Reconstruct and return _the queue that is represented by the input array_ `people`. The returned queue should be formatted as an array `queue`, where `queue[j] = [hj, kj]` is the attributes of the `jth` person in the queue (`queue[0]` is the person at the front of the queue).

## solutions

### sorting + nested loop

If we go by sorted order ascending, we know that we can leave space in front of us as everyone coming later will count towards being equal or taller to us.

```python
def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
	people.sort(key=lambda x: (x[0], x[1]))
	res = [None]*len(people)
	  
	for height, num_in_front in people:
		i = 0
		rem = num_in_front
		while rem > 0 or res[i] != None:
			if res[i] is None or res[i][0] == height:
				rem -= 1
				i += 1
			else:
				i += 1
		res[i] = [height, num_in_front]
	return res
```
