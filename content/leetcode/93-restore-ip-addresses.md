---
type: leetcode
title: 93. restore ip addresses
tags:
  - backtracking
  - recursion
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-18
updated: 2024-09-18
---

A **valid IP address** consists of exactly four integers separated by single dots. Each integer is between `0` and `255` (**inclusive**) and cannot have leading zeros.

- For example, `"0.1.2.201"` and `"192.168.1.1"` are **valid** IP addresses, but `"0.011.255.245"`, `"192.168.1.312"` and `"192.168@1.1"` are **invalid** IP addresses.

Given a string `s` containing only digits, return _all possible valid IP addresses that can be formed by inserting dots into_ `s`. You are **not** allowed to reorder or remove any digits in `s`. You may return the valid IP addresses in **any** order.

## solutions

Standard backtracking problem.

```python
def restoreIpAddresses(self, s: str) -> List[str]:
	res = []
	acc = []

	def recurse(idx, remaining):
		nonlocal res, acc

		# base case
		if idx == len(s) or remaining == 0:
			if idx == len(s) and remaining == 0:
				res.append(".".join(acc))
			return
	  
		# handle leading zero case
		if s[idx] == "0":
			acc.append("0")
			recurse(idx+1, remaining-1)
			acc.pop()
			return
	  
		next_val = ""
		for i in range(3):
			if idx+i >= len(s): break
	  
			next_val += s[idx+i]
			if int(next_val) > 255:
				break

			acc.append(next_val)
			recurse(idx+i+1, remaining-1)
			acc.pop()
	  
	recurse(0, 4)
	return res
```
