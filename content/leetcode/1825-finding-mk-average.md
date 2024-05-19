---
type: leetcode
title: 1825. finding mk average
tags:
  - array
  - binary-search
  - sliding-window
aliases: 
parents: 
children: 
supports:
  - "[[295-find-median-from-data-stream]]"
enemies: 
date: 2022-12-30
updated: 2024-05-18
---

You are given two integers, `m` and `k`, and a stream of integers. You are tasked to implement a data structure that calculates the **MKAverage** for the stream.

The **MKAverage** can be calculated using these steps:

1. If the number of the elements in the stream is less than `m` you should consider the **MKAverage** to be `-1`. Otherwise, copy the last `m` elements of the stream to a separate container.
2. Remove the smallest `k` elements and the largest `k` elements from the container.
3. Calculate the average value for the rest of the elements **rounded down to the nearest integer**.

Implement the `MKAverage` class:

- `MKAverage(int m, int k)` Initializes the **MKAverage** object with an empty stream and the two integers `m` and `k`.
- `void addElement(int num)` Inserts a new element `num` into the stream.
- `int calculateMKAverage()` Calculates and returns the **MKAverage** for the current stream **rounded down to the nearest integer**.

## solution

### brute force idea

Initially, the first idea that comes into my head, in terms of a brute force solution, is to maintain a window of length $m$ that stores the latest $m$ elements, and then for each query, we sort the array, remove the leftmost and rightmost $k$ elements, and then calculate the average.

The runtime of this approach is $O(1)$ for `addElement` (when using a `deque` for the list of length $m$). The runtime for `calculateMKAverage` is $O(m\log m + m)$, where we first sort and then calculate the sum of the middle elements.

### optimization idea #1

However, if we want to improve from this, we probably want a way to maintain a sorted representation of our data, instead of having to sort every time we call `calculateMKAverage`.

To do this, we can maintain an unsorted list of $m$ elements called `window`, as well as a sorted list of $m$ elements called `s`. Everytime we call `addElement`, we update our sliding window `window` in $O(1)$ time, and then update `s` in $O(\log m + m)$ time ($\log m$ to find the element to remove, and then $O(m)$ to remove the element).

Then, our queries will just require us to sum up the middle values in `s`, taking $O(m)$ time.

### optimization idea #2

Instead of maintaining one large sorted array `s` of length $m$, we can maintain three sorted arrays, called `lows`, `mids`, and `highs`. We store the lowest $k$ elements, the middle $m-2k$ elements, and highest $k$ elements respectively in these sorted lists.

Then, when we call `addElement`, we remove the oldest element (falling out of the window) and add the newer element. These processes will take $O(k + (m-2k))$ depending on where we’re adding to/removing from.

After removing a value, we shift the values down to maintain our invariance of sorting between the three lists. We guarantee that after `_remove` is run, we have one open space in `self.highs`.

Then, we run `_add`, inserting the number into the correct list, and shifting numbers right-ward if necessary.

Finally, we can still run queries in $O(m-2k)$ time.


> [!attention]- a note on the use of `SortedList`
> Instead of using normal Python lists, we use `SortedList` here as the implementation of `SortedList` achieves amortized $O(\log n)$ runtime on insertion/deletion, as lists are represented as a list of smaller lists internally.
>
> This improves the runtime of `addElement` to $O(\log(k) + \log(m-2k))$. For details, visit [here](https://grantjenks.com/docs/sortedcontainers/implementation.html).

```python
from sortedcontainers import SortedList

class MKAverage:
	def __init__(self, m: int, k: int):
		self.window = deque()
		self.lows = SortedList()
		self.mids = SortedList()
		self.highs = SortedList()
		self.m = m
		self.k = k
	
	def addElement(self, num: int) -> None:
		# this is only run once
		if len(self.window) + 1 == self.m:
			self.window.append(num)
			self._initializeLists()
		
		elif len(self.window) < self.m:
			self.window.append(num)
		
		else:
			# update sliding window and window sum
			to_remove = self.window.popleft()
			self.window.append(num)
			
			self._remove(to_remove)
			self._add(num)
	
	def calculateMKAverage(self) -> int:
		if len(self.window) < self.m:
			return -1
		return sum(self.mids) // (self.m - 2 * self.k)
		
	def _initializeLists(self):
		for i, num in enumerate(sorted(self.window)):
			if i < self.k:
				self.lows.add(num)
		
			elif i >= self.m-self.k:
				self.highs.add(num)
		
			else:
				self.mids.add(num)
	
	def _add(self, num):
		# assume groups always begin with one value
		# missing in high when this function is called
		if num >= self.mids[-1]:
			self.highs.add(num)
		
		elif num >= self.lows[-1]:
			self.mids.add(num)
			self.highs.add(self.mids.pop(-1))

		else:
			self.lows.add(num)
			self.mids.add(self.lows.pop(-1))
			self.highs.add(self.mids.pop(-1))
	
	def _remove(self, num):
		"""Remove num, then shift values left to fill"""
		# assume that groups are full to begin with
		
		if num <= self.lows[-1]:
			self.lows.remove(num) # O(logn)
			# shift left
			self.lows.add(self.mids.pop(0))
			self.mids.add(self.highs.pop(0))

		elif num >= self.highs[0]:
			self.highs.remove(num) # O(logn)

		else:
			self.mids.remove(num) # O(logn)
			self.mids.add(self.highs.pop(0))
```

### optimization idea #3

Instead of summing up the entirety of `mids` at query time, we can maintain a counter called `sum` that keeps track of the sum of `mids`. This code is slightly harder to read, but improves query time from $O(m-2k)$ to $O(1)$.

```python
from sortedcontainers import SortedList

class MKAverage:
	def __init__(self, m: int, k: int):
		self.window = deque()
		self.sum = 0
		self.lows = SortedList()
		self.mids = SortedList()
		self.highs = SortedList()
		self.m = m
		self.k = k
	
	def addElement(self, num: int) -> None:
		# this is only run once, just finished window
		if len(self.window) + 1 == self.m:
			self.window.append(num)
			self._initializeLists()

		# still building window
		elif len(self.window) < self.m:
			self.window.append(num)

		else:
			# update sliding window and window sum
			to_remove = self.window.popleft()
			self.window.append(num)
		
			self._remove(to_remove)
			self._add(num)
	
	def calculateMKAverage(self) -> int:
		if len(self.window) < self.m:
			return -1
		return self.sum // (self.m - 2 * self.k)
	
	def _initializeLists(self):
		for i, num in enumerate(sorted(self.window)):
			if i < self.k:
				self.lows.add(num)
			elif i >= self.m-self.k:
				self.highs.add(num)
			else:
				self.mids.add(num)
		
		self.sum = sum(self.mids)

	def _add(self, num):
		# assume groups always begin with one value
		# missing in high when this function is called
		if num >= self.mids[-1]:
			self.highs.add(num)
		elif num >= self.lows[-1]:
			self.mids.add(num)
			self.sum += num
		
			removed_mid = self.mids.pop(-1)
			self.sum -= removed_mid
			self.highs.add(removed_mid)
		else:
			self.lows.add(num)
			removed_low = self.lows.pop(-1)
			self.mids.add(removed_low)
			self.sum += removed_low
			removed_mid = self.mids.pop(-1)
			self.sum -= removed_mid
			self.highs.add(removed_mid)
	
	def _remove(self, num):
		"""Remove num, then shift values left to fill"""
		# assume that groups are full to begin with
		
		if num <= self.lows[-1]:
			self.lows.remove(num) # O(logn)
			# shift left
			removed_mid = self.mids.pop(0)
			self.lows.add(removed_mid)
			self.sum -= removed_mid
			removed_high = self.highs.pop(0)
			self.mids.add(removed_high)
			self.sum += removed_high
		elif num >= self.highs[0]:
			self.highs.remove(num) # O(logn)
		else:
			self.mids.remove(num) # O(logn)
			self.sum -= num
			removed_high = self.highs.pop(0)
			self.mids.add(removed_high)
			self.sum += removed_high
```
