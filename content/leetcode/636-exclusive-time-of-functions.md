---
type: leetcode
title: 636. exclusive time of functions
tags:
  - stack
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-17
updated: 2024-08-17
---

On a **single-threaded** CPU, we execute a program containing `n` functions. Each function has a unique ID between `0` and `n-1`.

Function calls are **stored in a [call stack](https://en.wikipedia.org/wiki/Call_stack)**: when a function call starts, its ID is pushed onto the stack, and when a function call ends, its ID is popped off the stack. The function whose ID is at the top of the stack is **the current function being executed**. Each time a function starts or ends, we write a log with the ID, whether it started or ended, and the timestamp.

You are given a list `logs`, where `logs[i]` represents the `ith` log message formatted as a string `"{function_id}:{"start" | "end"}:{timestamp}"`. For example, `"0:start:3"` means a function call with function ID `0` **started at the beginning** of timestamp `3`, and `"1:end:2"` means a function call with function ID `1` **ended at the end** of timestamp `2`. Note that a function can be called **multiple times, possibly recursively**.

A function's **exclusive time** is the sum of execution times for all function calls in the program. For example, if a function is called twice, one call executing for `2` time units and another call executing for `1` time unit, the **exclusive time** is `2 + 1 = 3`.

Return _the **exclusive time** of each function in an array, where the value at the_ `ith` _index represents the exclusive time for the function with ID_ `i`.

## solution

Use a stack to keep track of which task currently has the exclusive time. Look at each command in context with the previous command to determine the amount of time units that the active command received. (It’s different in the cases of start/start, start/end, end/start, end/end because of how the indexing ends up working out).

I originally thought we could just keep a stack of commands and pop them when we saw an “end” command, but that breaks in the case of this test case:

![[636-exclusive-time-of-functions.png]]

```python
def exclusiveTime(self, n: int, logs: List[str]) -> List[int]:
	stack = []
	times = [0]*n
	  
	ptask, pc, pt = None, None, None
	for i, log in enumerate(logs):
		task_id, command, time = log.split(":")
		task_id = int(task_id)
		time = int(time)
		  
		# first task case
		if len(stack) == 0:
			stack.append(task_id)
			ptask, pc, pt = task_id, command, time
			continue
		  
		if command == "start":
			if pc == "start":
				times[stack[-1]] += time-pt
			else:
				times[stack[-1]] += time-pt-1
			stack.append(task_id)
		else: # end
			if pc == "start":
				times[stack[-1]] += time-pt+1
			else:
				times[stack[-1]] += time-pt
			stack.pop()
		  
		ptask, pc, pt = task_id, command, time

	return times
```
