---
type: leetcode
title: 362. design hit counter
tags:
  - queue
  - binary-search
date: 2022-12-29
updated: 2024-08-01
---

Design a hit counter which counts the number of hits received in the past `5` minutes (i.e., the past `300` seconds).

Your system should accept a `timestamp` parameter (**in seconds** granularity), and you may assume that calls are being made to the system in chronological order (i.e., `timestamp` is monotonically increasing). Several hits may arrive roughly at the same time.

Implement the `HitCounter` class:

- `HitCounter()` Initializes the object of the hit counter system.
- `void hit(int timestamp)` Records a hit that happened at `timestamp` (**in seconds**). Several hits may happen at the same `timestamp`.
- `int getHits(int timestamp)` Returns the number of hits in the past 5 minutes from `timestamp` (i.e., the past `300` seconds).

## solutions

### queue w/ hashmap

My initial idea was to keep track of the timestamps in a queue, adding to the right, and then delete the oldest ones from the left when the newest `timestamp` seen is out of the 300 second range.

Then, as an optimization, I keep track of a running total, although equally, we could just not do that and return `len(self.timestamps)` in `getHits`.

This gives us $O(1)$ time for `hit` and worst-case $O(n)$ for `getHits`.

```python
class HitCounter:
	def __init__(self):
		self.timestamps = deque()
		self.total = 0
	  
	def hit(self, timestamp: int) -> None:
		self.timestamps.append(timestamp)
		self.total += 1
	  
	def getHits(self, timestamp: int) -> int:
		while len(self.timestamps) and self.timestamps[0] <= (timestamp-300):
			removed_timestamp = self.timestamps.popleft()
			self.total -= 1
		return self.total
```

#### just a queue

```python
class HitCounter:
	def __init__(self):
		self.timestamps = deque()
	  
	def hit(self, timestamp: int) -> None:
		self.timestamps.append(timestamp)
	  
	def getHits(self, timestamp: int) -> int:
		while len(self.timestamps) and self.timestamps[0] <= (timestamp-300):
			self.timestamps.popleft()
		return len(self.timestamps)
```

### array w/ binary search

Instead of linearly removing elements that have fallen out of the window, we can just maintain the entire window, and do a binary search for the left bound whenever we call `getHits`.

This lets us improve the worst-case runtime of `getHits` to $O(\log n)$.

```python
class HitCounter:
	def __init__(self):
		self.a = [float("-inf")]

	def hit(self, timestamp: int) -> None:
		self.a.append(timestamp)

	def getHits(self, timestamp: int) -> int:
		bottom_bound = bisect.bisect_right(self.a, timestamp-300)
		return len(self.a) - bottom_bound
```
