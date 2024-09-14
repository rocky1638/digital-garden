---
type: leetcode
title: 282. expression add operators
tags:
  - backtracking
  - recursion
  - math
aliases: 
parents:
  - "[[227-basic-calculator-ii]]"
children: 
supports: 
enemies: 
date: 2024-09-01
updated: 2024-09-01
---

Given a string `num` that contains only digits and an integer `target`, return _**all possibilities** to insert the binary operators_ `'+'`_,_ `'-'`_, and/or_ `'*'` _between the digits of_ `num` _so that the resultant expression evaluates to the_ `target` _value_.

Note that operands in the returned expressions **should not** contain leading zeros.

## solutions

Here, I do a recursion where at each step we add an operator, or don’t and continue the number.

Then, I run [[227-basic-calculator-ii]] on every resulting string and check to see if the value matches `target`.

```python
def addOperators(self, num: str, target: int) -> List[str]:
	"""
	at each index, we can add +, -, *, or nothing to space;
	  
	* has precedence... how do we do this recursively...
	- just enumerate every possibility and calculate it once we
	reach the end of a recursion?
	"""
	  
	res = []
	acc = [num[0]]

	def recurse(idx, can_append_op, first_in_group):
		if idx == len(num):
			val = self.calculate("".join(acc))
			if val == target:
				res.append("".join(acc))
				return
	  
		if can_append_op:
			for op in ["+", "-", "*"]:
				acc.append(op)
				recurse(idx, False, None)
				acc.pop()
	  
		if first_in_group != "0":
			# skip
			acc.append(num[idx])
			recurse(idx+1, True, first_in_group or num[idx])
			acc.pop()
	  
	recurse(1, True, num[0])
	return res
```

There’s two optimizations that can be made to the above solution:

1. We can try every possible number from our current recursion `idx` to end, instead of creating a new function call in the stack for the “skip” cases above.
2. Instead of computing values at the end (which I opted to do because it’s hard to handle multiplication as it has a higher precedence), we can just keep track of our previous value, and when we see a multiplication, we can undo our last add/subtract of the previous value, and re-add our current value * previous value.
	- This is the same idea as in [[227-basic-calculator-ii]], where we pop the top value of the stack and push that value * current value when we see a multiplication operation.

Also, intuition is that at each number, we choose an operation to be to the left of it. The first number must have an implicit “+” to the left of it.

```python
def addOperators(self, num: str, target: int) -> List[str]:
	res = []
	def backtracking(ind, path, cur_sum, last_value):
		# base case
		if ind==len(num):
			if cur_sum==target: res.append(path)
			return

		# try every possible number starting at ind
		for i in range(ind, len(num)):
			cur_str = num[ind:i+1]
			cur_val = int(cur_str)

			# leading zero numbers not allowed
			if num[ind]=='0' and i>ind:
				break

			# first number can't have operation before it
			if ind==0:
				backtracking(i+1, cur_str, cur_val, cur_val)
			else:
				backtracking(i+1, path+'-'+cur_str, cur_sum-cur_val, -cur_val)
				backtracking(i+1, path+'+'+cur_str, cur_sum+cur_val, cur_val)
				backtracking(i+1, path+'*'+cur_str, cur_sum-last_value+last_value*cur_val, last_value*cur_val)
	
	return backtracking(0,'',0,0) return res

```
