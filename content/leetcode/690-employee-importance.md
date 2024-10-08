---
type: leetcode
title: 690. employee importance
tags:
  - dfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-24
---

You have a data structure of employee information, including the employee's unique ID, importance value, and direct subordinates' IDs.

You are given an array of employees `employees` where:

- `employees[i].id` is the ID of the `ith` employee.
- `employees[i].importance` is the importance value of the `ith` employee.
- `employees[i].subordinates` is a list of the IDs of the direct subordinates of the `ith` employee.

Given an integer `id` that represents an employee's ID, return _the **total** importance value of this employee and all their direct and indirect subordinates_.

## solution

Pretty basic recursion/DFS. Use a hashmap for fast employee lookup.

```python
def getImportance(self, employees: List['Employee'], id: int) -> int:
	# construct hashmap for O(1) lookup
	d = {}
	for employee in employees:
		d[employee.id] = employee
	  
	def dfs(eid):
		res = d[eid].importance
		for subordinate in d[eid].subordinates:
			res += dfs(subordinate)
	
		return res
	  
	return dfs(id)
```
