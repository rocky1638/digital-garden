---
type: leetcode
title: 39. combination sum
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/combination-sum/
date: 2022-11-21
updated: 2024-08-23
tags:
  - backtracking
  - recursion
---

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

## solution

This is classic backtracking, where we try to assemble valid combinations from the top-down.

With each recursive call, we go through the list of candidates in order, either choosing to append the current candidate again, or to append the next candidate. If our tally ever equals the target, we take the valid combination and append it to `ans`. Else, if our tally is past the target, we can just stop that branch of the backtracking.

```python
def combinationSum(self, candidates: List[int], target: int):
	acc = []
	total = 0

	def recurse(idx):
		nonlocal total
		if total == target:
			return [acc[:]]
		if idx == len(candidates) or total > target:
			return []

		res = []
	  
		# take value, don't progress
		acc.append(candidates[idx])
		total += candidates[idx]
		res.extend(recurse(idx))
		total -= candidates[idx]
		acc.pop()
	  
		# stop taking value, progress
		res.extend(recurse(idx+1))
	  
		return res
	return recurse(0)
```
