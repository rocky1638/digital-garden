---
type: leetcode
title: "946. validate stack sequences"
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-04-04
---

Given two integer arrays `pushed` and `popped` each with distinct values, return `true` _if this could have been the result of a sequence of push and pop operations on an initially empty stack, or_ `false` _otherwise._

## solution

We simulate the operations, greedily popping values if we can _(we always do this before pushing more values, because if we push more values, we won’t be able to pop the current value without first popping other values)._

```python
def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
	pushed_ptr = 0
	popped_ptr = 0
	  
	stack = []
	  
	while pushed_ptr < len(pushed) or popped_ptr < len(popped):
		while len(stack) and stack[-1] == popped[popped_ptr]:
			stack.pop()
			popped_ptr += 1
	  
		# we've pushed everything, but we were unable to
		# fully execute all the pop operations above.
		if pushed_ptr == len(pushed):
			return popped_ptr == len(popped)
	  
		stack.append(pushed[pushed_ptr])
		pushed_ptr += 1
	  
	return True
```
