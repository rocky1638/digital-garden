---
type: leetcode
title: 227. basic calculator ii
tags:
  - string
  - stack
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-28
updated: 2024-08-28
---

Given a string `s` which represents an expression, _evaluate this expression and return its value_. 

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of `[-231, 231 - 1]`.

**Note:** You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

## solution

Very similar logic to [[224-basic-calculator]], but instead of recursing inside of brackets, we just use a stack and always compute multiplication/division when we see it. Then, the numbers left just need to be added/subtracted, to maintain BEDMAS.

```python
def calculate(self, s: str) -> int:
	def parse_number(i):
		res = 0
		while i < len(s) and s[i].isnumeric():
			res *= 10
			res += int(s[i])
			i += 1
		return i, res

	def compute(x, y, op):
		if op == "*":
			return x * y
		elif op == "/":
			return int(x / y)
  
	i = 0
	prev_op = "+"
	stack = []
	while i < len(s):
		if s[i].isnumeric():
			i, val = parse_number(i)
	  
			if prev_op == "+":
				stack.append(val)
			elif prev_op == "-":
				stack.append(-val)
			else: # * or /
				stack[-1] = compute(stack[-1], val, prev_op)
	  
		elif s[i] in {"+", "-", "*", "/"}:
			prev_op = s[i]
			i += 1
		else:
			i += 1
	  
	return sum(stack)
```
