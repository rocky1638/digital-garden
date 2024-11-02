---
type: leetcode
title: 65. valid number
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-22
updated: 2024-10-22
---

Given a string `s`, return whether `s` is a **valid number**.

For example, all the following are valid numbers: `"2", "0089", "-0.1", "+3.14", "4.", "-.9", "2e10", "-90E3", "3e+7", "+6e-1", "53.5e93", "-123.456e789"`, while the following are not valid numbers: `"abc", "1a", "1e", "e3", "99e2.5", "--6", "-+3", "95a54e53"`.

Formally, a **valid number** is defined using one of the following definitions:

1. An **integer number** followed by an **optional exponent**.
2. A **decimal number** followed by an **optional exponent**.

An **integer number** is defined with an **optional sign** `'-'` or `'+'` followed by **digits**.

A **decimal number** is defined with an **optional sign** `'-'` or `'+'` followed by one of the following definitions:

1. **Digits** followed by a **dot** `'.'`.
2. **Digits** followed by a **dot** `'.'` followed by **digits**.
3. A **dot** `'.'` followed by **digits**.

An **exponent** is defined with an **exponent notation** `'e'` or `'E'` followed by an **integer number**.

The **digits** are defined as one or more digits.

## solutions

### modular

```python
def isNumber(self, s: str) -> bool:
	def valid_integer(ss):
		seen_digit = False
		for i in range(len(ss)):
			if ss[i] in {"-", "+"}:
				if i > 0: return False
			elif ss[i].isdigit():
				seen_digit = True
			else:
			return False
		return seen_digit
	  
	def valid_decimal(ss):
		seen_dot = False
		seen_digit = False
		for i in range(len(ss)):
			if ss[i] in {"-", "+"}:
				if i > 0: return False
			elif ss[i].isdigit():
				seen_digit = True
			elif ss[i] == ".":
				if seen_dot: # only one dot
					return False
				seen_dot = True
			else:
				return False
		return seen_digit
	  
	s = s.lower()
	parts = s.split("e")
	  
	if len(parts) > 2:
		return False
	  
	# first part integer or decimal
	valid = valid_integer(parts[0]) or valid_decimal(parts[0])
	  
	# handle exponent
	if len(parts) == 2:
		valid = valid and valid_integer(parts[1])
	  
	return valid
```

### dfa

todo
