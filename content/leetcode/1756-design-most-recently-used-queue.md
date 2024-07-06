---
type: leetcode
title: 1756. design most recently used queue
tags:
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-23
---

Design a queue-like data structure that moves the most recently used element to the end of the queue.

Implement the `MRUQueue` class:

- `MRUQueue(int n)` constructs the `MRUQueue` with `n` elements: `[1,2,3,...,n]`.
- `int fetch(int k)` moves the `kth` element **(1-indexed)** to the end of the queue and returns it.

## solutions

### brute force (list)

This solution achieves $O(n)$ initialization and $O(n)$ per fetch (to shift down every value in the list).

```python
class MRUQueue:
	def __init__(self, n: int):
		self.queue = [x for x in range(1, n+1)]

	def fetch(self, k: int) -> int:
		self.queue.append(self.queue.pop(k-1))
		return self.queue[-1]
```

### sorted list (binary search tree)

Using a `SortedList`, we keep track of value and “effective index”. Instead of changing the index values after fetching (to slide values left), we just keep a counter called `next_idx` that we keep increasing.

```python
from sortedcontainers import SortedList

class MRUQueue:
	def __init__(self, n: int):
		# queue[k] = (k, val)
		self.queue = SortedList([(x, x) for x in range(1, n+1)])
		self.next_idx = n+1
		  
	def fetch(self, k: int) -> int:
		popped_idx, val = self.queue.pop(k-1)
		  
		self.queue.add((self.next_idx, val))
		self.next_idx += 1
		  
		return val
```
