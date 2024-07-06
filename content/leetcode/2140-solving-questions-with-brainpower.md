---
type: leetcode
title: 2140. solving questions with brainpower
tags:
  - dp
  - backtracking
  - memoization
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-30
---

You are given a **0-indexed** 2D integer array `questions` where `questions[i] = [pointsi, brainpoweri]`.

The array describes the questions of an exam, where you have to process the questions **in order** (i.e., starting from question `0`) and make a decision whether to **solve** or **skip** each question. Solving question `i` will **earn** you `pointsi` points but you will be **unable** to solve each of the next `brainpoweri` questions. If you skip question `i`, you get to make the decision on the next question.

- For example, given `questions = [[3, 2], [4, 3], [4, 4], [2, 5]]`:
    - If question `0` is solved, you will earn `3` points but you will be unable to solve questions `1` and `2`.
    - If instead, question `0` is skipped and question `1` is solved, you will earn `4` points but you will be unable to solve questions `2` and `3`.

Return _the **maximum** points you can earn for the exam_.

## solutions

### top-down recursion w/ memoization

At each step, we can choose to solve the question or skip it. This translates pretty easily into a backtracking/recursive solution. We realize that all we care about is the current index that we are positioned at, so that’s the only necessary parameter to `recurse`.

```python
def mostPoints(self, questions: List[List[int]]) -> int:
	n = len(questions)
	memo = {}
	  
	def recurse(idx):
		if idx >= n:
			return 0
		  
		if idx in memo:
			return memo[idx]
		  
		best = 0
		  
		# skip question
		best = max(best, recurse(idx+1))
		  
		# solve question
		best = max(
			best,
			questions[idx][0] + recurse(idx + questions[idx][1]+1)
		)
		  
		memo[idx] = best
		return best
	  
	return recurse(0)
```

### top-down dynamic programming

We can convert the logic used above into a similar dynamic programming solution by iterating backwards through our DP array and populating the values using the same recurrence relationship as above.

```python
def mostPoints(self, questions: List[List[int]]) -> int:
	n = len(questions)
	# dp[i] = best score starting at index i
	dp = [0]*n
	# base case, starting at last index
	dp[-1] = questions[-1][0]
	  
	for i in reversed(range(n-1)):
		skip_score = dp[i+1]
		solve_score = questions[i][0]
		if i+questions[i][1]+1 < n:
			solve_score += dp[i+questions[i][1]+1]
		dp[i] = max(skip_score, solve_score)
	return dp[0]
```
