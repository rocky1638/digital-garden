---
type: leetcode
title: 1711. count good meals
tags:
  - hashmap
  - array
aliases: 
parents:
  - "[[1-two-sum]]"
children: 
supports: 
enemies: 
date: 2024-10-19
updated: 2024-10-19
---

A **good meal** is a meal that contains **exactly two different food items** with a sum of deliciousness equal to a power of two.

You can pick **any** two different foods to make a good meal.

Given an array of integers `deliciousness` where `deliciousness[i]` is the deliciousness of the `i​​​​​​th​​​​`​​​​ item of food, return _the number of different **good meals** you can make from this list modulo_ `109 + 7`.

Note that items with different indices are considered different even if they have the same deliciousness value.

## solution

We realize that there are only 21 possible powers of two that could be summed to, so we can just run [[1-two-sum]] for each of them.

```python
# O(22n) ~= O(n)
def countPairs(self, deliciousness: List[int]) -> int:
	def two_sum(target):
		acc = 0
		# { val: count }
		seen = defaultdict(int)
	  
		for num in deliciousness:
			acc += seen[target-num]
			seen[num] += 1
		return acc
	  
	res = 0
	for power in range(0, 22):
		target = 2 ** power
		res += two_sum(target)
	return res % (10**9+7)
```
