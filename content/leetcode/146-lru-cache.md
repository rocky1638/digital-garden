---
type: leetcode
title: 146. lru cache
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/lru-cache/
date: 2022-11-23
updated: 2024-08-18
tags:
  - linked-list
  - hashmap
---

Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

## solution

We use a linked list, more specifically, a doubly linked list to keep the nodes in the order of most recently used.

Then, to enable constant-time lookup of a particular node in the DLL by key, use a hashmap to map the `key` values to the nodes in the list.

```python
class DLL:
	def __init__(self):
		# head <---> tail
		# head is most recent, tail is least
		self.head = DLLNode(None,None)
		self.tail = DLLNode(None,None)
		self.head.right = self.tail
		self.tail.left = self.head

	def insert_at_head(self, node):
		nex = self.head.right
		self.head.right = node
		node.left = self.head
		node.right = nex
		nex.left = node

	def remove_node(self, node):
		prev, nex = node.left, node.right
  
		prev.right = nex
		nex.left = prev

	def remove_at_tail(self):
		key = self.tail.left.key
		self.remove_node(self.tail.left)
		return key

	def __str__(self):
		res = ""
		cur = self.head.right
		while cur != self.tail:
			res += f"left: {cur.left.val} --- {cur.key}, {cur.val} --- right: {cur.right.val}"
			res += "\n"
			cur = cur.right
		return res

class DLLNode:
	def __init__(self, key, val):
		self.key = key
		self.val = val
		self.left = None
		self.right = None
  
class LRUCache:
	def __init__(self, capacity: int):
		self.DLL = DLL()
		# key: Node
		self.d = {}
		self.capacity = capacity
		self.size = 0

	def _move_node_to_head(self, node):
		self.DLL.remove_node(node)
		self.DLL.insert_at_head(node)
  
	def get(self, key: int) -> int:
		if key not in self.d:
			return -1
  
		node = self.d[key]
		self._move_node_to_head(node)
		  
		return node.val
  
def put(self, key: int, value: int) -> None:
	if key in self.d:
		self.d[key].val = value
		self._move_node_to_head(node)
		return

	new_node = DLLNode(key, value)
  
	self.d[key] = new_node
	self.DLL.insert_at_head(new_node)
	self.size += 1
  
	if self.size > self.capacity:
		popped_key = self.DLL.remove_at_tail()
		del self.d[popped_key]
		self.size -= 1
```
