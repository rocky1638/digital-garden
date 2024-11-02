---
type: leetcode
title: 1106. parsing a boolean expression
tags:
  - recursion
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-25
updated: 2024-10-25
---

A **boolean expression** is an expression that evaluates to either `true` or `false`. It can be in one of the following shapes:

- `'t'` that evaluates to `true`.
- `'f'` that evaluates to `false`.
- `'!(subExpr)'` that evaluates to **the logical NOT** of the inner expression `subExpr`.
- `'&(subExpr1, subExpr2, ..., subExprn)'` that evaluates to **the logical AND** of the inner expressions `subExpr1, subExpr2, ..., subExprn` where `n >= 1`.
- `'|(subExpr1, subExpr2, ..., subExprn)'` that evaluates to **the logical OR** of the inner expressions `subExpr1, subExpr2, ..., subExprn` where `n >= 1`.

Given a string `expression` that represents a **boolean expression**, return _the evaluation of that expression_.

It is **guaranteed** that the given expression is valid and follows the given rules.

## solution

Very similar to [[224-basic-calculator]].

```python
def parseBoolExpr(self, expression: str) -> bool:
	def eval_op(bools, op):
		if op == "!":
			return not bools[0]
		elif op == "&":
			return all([b for b in bools])
		elif op == "|":
			return any([b for b in bools])
	  
	def parse(idx) -> tuple[list[bool], int]:
		i = idx
		bools = []
		op = None
	  
		while i < len(expression):
			c = expression[i]
		  
			if c == "t":
				bools.append(True)
				i += 1
			elif c == "f":
				bools.append(False)
				i += 1
			elif c in {"|", "!", "&"}:
				op = c
				i += 1
			elif c == "(":
				inner_bools, next_idx = parse(i+1)
				bools.append(eval_op(inner_bools, op))
				i = next_idx
				op = None
			elif c == ")":
				return bools, i+1
			else:
				i += 1
	  
		return bools, i
	  
	return parse(0)[0][0]
```
