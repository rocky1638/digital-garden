---
type: leetcode
title: 729. my calendar i
tags:
  - binary-search-tree
  - binary-search
  - intervals
aliases: 
parents:
  - "[[56-merge-intervals]]"
children: 
supports: 
enemies: 
date: 2024-08-10
updated: 2024-08-10
---

You are implementing a program to use as your calendar. We can add a new event if adding the event will not cause a **double booking**.

A **double booking** happens when two events have some non-empty intersection (i.e., some moment is common to both events.).

The event can be represented as a pair of integers `start` and `end` that represents a booking on the half-open interval `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

Implement the `MyCalendar` class:

- `MyCalendar()` Initializes the calendar object.
- `boolean book(int start, int end)` Returns `true` if the event can be added to the calendar successfully without causing a **double booking**. Otherwise, return `false` and do not add the event to the calendar.

## solutions

### binary search

We can maintain a list of sorted ranges, and then when we try to add a new range, binary search to find the insertion index, and check the neighboring ranges for overlap.

Note that because we are guaranteed that the existing array is disjoint, the only two intervals that can overlap are the neighboring ones.

This solution has $O(\log n)$ lookup, but inserting into the array takes linear time.

```python
class MyCalendar:
	def __init__(self):
		self.bookings = []
	  
	def book(self, start: int, end: int) -> bool:
		if not self.bookings:
			self.bookings.append((start, end))
			return True

	insertion_point = bisect_left(self.bookings, (start, end))
	  
	valid = True
	if insertion_point > 0 and self.bookings[insertion_point-1][1] > start:
		valid = valid and False
	if insertion_point < len(self.bookings) and self.bookings[insertion_point][0] < end:
		valid = valid and False
	  
	if valid:
		self.bookings.insert(insertion_point, (start, end))
	return valid
```

### binary search tree w/ ranges

Instead of using a sorted array, maintain a binary search tree to allow for $O(\log n)$ insertion.

```python
class Node:
	def __init__(self, start, end):
		self.start = start
		self.end = end
		self.left = None
		self.right = None

	def insert(self, node):
		# starts after current node
		if node.start >= self.end:
			if not self.right:
				self.right = node
				return True
			return self.right.insert(node)
		# ends before current node
		elif node.end <= self.start:
			if not self.left:
				self.left = node
				return True
			return self.left.insert(node)
		return False
  
class MyCalendar:
	def __init__(self):
		self.root = None

	def book(self, start: int, end: int) -> bool:
		if not self.root:
			self.root = Node(start, end)
			return True
		return self.root.insert(Node(start, end))
```
