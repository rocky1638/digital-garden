---
type: leetcode
title: 301. remove invalid parentheses
tags:
  - backtracking
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-10
updated: 2024-09-10
---

Given a string `s` that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.

Return _a list of **unique strings** that are valid with the minimum number of removals_. You may return the answer in **any order**.

## solutions

### naive backtracking w/ early stopping

We can just try to take/skip every bracket. We can have a small optimization to avoid adding a closing bracket if `balance` is already at `0`.

```python
def removeInvalidParentheses(self, s: str) -> List[str]:
	res = set()
	acc = []
	balance = 0
	best_len = 0

	def recurse(idx):
		nonlocal balance, res, acc, best_len
		# base cases
		if idx == len(s) and balance == 0:
			if len(res) == 0 or len(acc) > best_len:
				best_len = len(acc)
				res.clear()
				res.add("".join(acc[:]))
			elif len(acc) == best_len:
				res.add("".join(acc))
			return
	  
		if idx == len(s):
			return
	  
		char = s[idx]
	  
		# non-bracket chars
		if char.isalpha():
			acc.append(char)
			recurse(idx+1)
			acc.pop()
	  
		# take
		elif char == "(":
			acc.append("(")
			balance += 1
			recurse(idx+1)
			balance -= 1
			acc.pop()
		elif char == ")" and balance > 0:
			acc.append(")")
			balance -= 1
			recurse(idx+1)
			balance += 1
			acc.pop()

		# leave
		recurse(idx+1)

	recurse(0)
	return res
```

### improved pruning

We can improve our pruning by first calculating how many left and right brackets we need to remove in $O(n)$ time - [[1249-minimum-remove-to-make-valid-parentheses]]. The rest of the recursion is similar, although we only skip a bracket if we still have `l_rem` or `r_rem` to remove.

```python
def getBracketsToRemove(self, s: str):
	r = 0
	balance = 0
	for char in s:
		if char == "(":
			balance += 1
		elif char == ")":
			if balance == 0:
				r += 1
			else:
				balance -= 1
	return balance, r        

def removeInvalidParentheses(self, s: str) -> List[str]:
	l_rem, r_rem = self.getBracketsToRemove(s)
	balance = 0
	res = set()
	acc = []
	def recurse(idx):
		nonlocal balance, res, acc, l_rem, r_rem
		# base cases
		if idx == len(s):
			if l_rem == 0 and r_rem == 0:
				res.add("".join(acc))
			return

		char = s[idx]

		# non-bracket chars
		if char.isalpha():
			acc.append(char)
			recurse(idx+1)
			acc.pop()
		
		# take
		elif char == "(":
			acc.append("(")
			balance += 1
			recurse(idx+1)
			balance -= 1
			acc.pop()
		elif char == ")" and balance > 0:
			acc.append(")")
			balance -= 1
			recurse(idx+1)
			balance += 1
			acc.pop()
		
		# leave
		if char == "(" and l_rem > 0:
			l_rem -= 1
			recurse(idx+1)
			l_rem += 1
		elif char == ")":
			r_rem -= 1
			recurse(idx+1)
			r_rem += 1

	recurse(0)
	return res
```
