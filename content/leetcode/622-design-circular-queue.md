---
type: leetcode
title: 622. design circular queue
tags:
  - linked-list
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-14
updated: 2024-09-14
---

Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle, and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

Implement the `MyCircularQueue` class:

- `MyCircularQueue(k)` Initializes the object with the size of the queue to be `k`.
- `int Front()` Gets the front item from the queue. If the queue is empty, return `-1`.
- `int Rear()` Gets the last item from the queue. If the queue is empty, return `-1`.
- `boolean enQueue(int value)` Inserts an element into the circular queue. Return `true` if the operation is successful.
- `boolean deQueue()` Deletes an element from the circular queue. Return `true` if the operation is successful.
- `boolean isEmpty()` Checks whether the circular queue is empty or not.
- `boolean isFull()` Checks whether the circular queue is full or not.

You must solve the problem without using the built-in queue data structure in your programming language.

## solution

Pretty basic solution using a doubly linked list.

The intuition is that we want access to the front and back of a data structure (with constant pop/append), and we don’t want to be bounded by a fixed array memory allocation.

The “circular” part of this is kind of just a red herring.

```python
class Node:
	def __init__(self, val):
		self.val = val
		self.prev = None
		self.next = None
	  
class MyCircularQueue:
	def __init__(self, k: int):
		# front --- rear
		self.capacity = k
		self.size = 0
		self.front = Node(0)
		self.rear = Node(0)
	  
		self.front.next = self.rear
		self.rear.prev = self.front
	  
	def enQueue(self, value: int) -> bool:
		if self.size == self.capacity:
			return False
	  
		node = Node(value)
		temp = self.rear.prev
	  
		temp.next = node
		node.prev = temp
		self.rear.prev = node
		node.next = self.rear
	  
		self.size += 1
	  
		return True
	  
	def deQueue(self) -> bool:
		if self.size == 0:
			return False
	  
		temp = self.front.next.next
		self.front.next = temp
		temp.prev = self.front
		  
		self.size -= 1
		  
		return True
	  
	def Front(self) -> int:
		if self.size == 0:
			return -1
		return self.front.next.val
	  
	def Rear(self) -> int:
		if self.size == 0:
			return -1
		return self.rear.prev.val
	  
	def isEmpty(self) -> bool:
		return self.size == 0
	  
	def isFull(self) -> bool:
		return self.capacity == self.size
```
