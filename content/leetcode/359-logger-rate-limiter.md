---
type: leetcode
title: "359. logger rate limiter"
tags:
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-19
---

Design a logger system that receives a stream of messages along with their timestamps. Each **unique** message should only be printed **at most every 10 seconds** (i.e. a message printed at timestamp `t` will prevent other identical messages from being printed until timestamp `t + 10`).

All messages will come in chronological order. Several messages may arrive at the same timestamp.

Implement the `Logger` class:

- `Logger()` Initializes the `logger` object.
- `bool shouldPrintMessage(int timestamp, string message)` Returns `true` if the `message` should be printed in the given `timestamp`, otherwise returns `false`.

## solution

This one is pretty simple, we just use a dictionary to keep track of the last timestamp that each message was sent at.

```python
class Logger:
	def __init__(self):
		# self.messages["message"] = last timestamp when message was sent
		self.messages = {}
	  
	def shouldPrintMessage(self, timestamp: int, message: str) -> bool:
		if message not in self.messages:
			self.messages[message] = timestamp
			return True
		else:
			if self.messages[message] > timestamp - 10:
				return False
			else:
				self.messages[message] = timestamp
				return True
```
