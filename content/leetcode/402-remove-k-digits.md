---
type: leetcode
title: 402. remove k digits
tags:
  - monotonic-stack
  - greedy
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-06
updated: 2024-07-06
---

Given string num representing a non-negative integer `num`, and an integer `k`, return _the smallest possible integer after removing_ `k` _digits from_ `num`.

## solution

After quickly realizing that backtracking is not feasible given that `num` can be up to length of $10^5$, we need to find a heuristic that works for any number, starting from `k=1`.

There are two main intuitions:

1. The further left a digit is, the more valuable it is to remove, because we have more potential to realize a bigger subtraction in the total value of the number.
2. If two adjacent digits $A$ and $B$ are such that $A$ is to the left of $B$ and $A > B$, then we greedily must remove $A$ to reach the optimal solution. This is because if we don’t do this, no matter what we do later in the right side of the string, we will get a worse answer compared to if we did it.

With this intuition, the solution can be coded using a monotonic stack approach, keeping in mind edge cases for leading zeroes and a purely monotonically increasing sequence.

```python
def removeKdigits(self, num: str, k: int) -> str:
	if num == 0: return 0
	  
	n = len(num)
	stack = []
	  
	for i in range(n):
		while stack and stack[-1] > num[i] and k > 0:
			stack.pop()
			k -= 1
	  
		stack.append(num[i])

	# if there was no "cliff", we need to pop the largest numbers
	while k > 0:
		stack.pop()
		k -= 1

	# zero cases
	if len(stack) == 0 or all([x == "0" for x in stack]):
		return "0"
	  
	# handle leading zeroes
	start_idx = 0
	while start_idx < len(stack) and stack[start_idx] == "0":
		start_idx += 1

	return "".join(stack[start_idx:])
```
