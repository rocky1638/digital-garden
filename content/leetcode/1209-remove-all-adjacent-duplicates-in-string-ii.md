---
type: leetcode
title: 1209. remove all adjacent duplicates in string ii
date: 2022-11-17
updated: 2024-09-14
tags:
  - stack
---

You are given a string `s` and an integer `k`, a `k` **duplicate removal** consists of choosing `k` adjacent and equal letters from `s` and removing them, causing the left and the right side of the deleted substring to concatenate together.

We repeatedly make `k` **duplicate removals** on `s` until we no longer can.

Return _the final string after all such duplicate removals have been made_. It is guaranteed that the answer is **unique**.

## solution

- we keep pushing each new character into a stack, and delete all blocks of `k` characters as they come up.
- we store tuples of `[char, count]` instead of just characters in order to improve the speed of checking for blocks from $O(n)$ to $O(1)$.

```python
def removeDuplicates(self, s: str, k: int) -> str:
	stack = []
	for char in s:
		if not stack or stack[-1][0] != char:
			stack.append([char, 1])
		else:
			stack[-1][1] += 1
			if stack[-1][1] == k:
				stack.pop()
	return "".join(char*freq for char, freq in stack)
```
