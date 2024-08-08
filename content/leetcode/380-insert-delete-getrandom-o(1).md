---
type: leetcode
title: 380. insert delete getrandom o(1)
date: 2022-11-16
updated: 2024-08-01
tags:
  - hashmap
  - array
---

Implement the `RandomizedSet` class:

- `RandomizedSet()` Initializes the `RandomizedSet` object.
- `bool insert(int val)` Inserts an item `val` into the set if not present. Returns `true` if the item was not present, `false` otherwise.
- `bool remove(int val)` Removes an item `val` from the set if present. Returns `true` if the item was present, `false` otherwise.
- `int getRandom()` Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the **same probability** of being returned.

You must implement the functions of the class such that each function works in **average** `O(1)` time complexity.

## solutions

### naive approach w/ set

We just keep a set, but the conversion to a `list` in `getRandom` is $O(n)$.

```python
class RandomizedSet:
	def __init__(self):
		self.set = set()

	def insert(self, val: int) -> bool:
		if val in self.set:
			return False

			self.set.add(val)
			return True

	def remove(self, val: int) -> bool:
		if val in self.set:
			self.set.remove(val)
			return True

		return False

	# this doesn't work because it's O(n)!
	def getRandom(self) -> int:
		return random.choice(list(self.set))
```

### array + hashmap w/ constant time deletion

We manually keep track of our values in a pseudo-set by combining a hashmap and an array.

This way, we don’t have to convert our set to an array everytime `getRandom` is called.

The main trick that allows us to do this while keeping `remove` constant time is by taking advantage of the fact that we don’t need to maintain any order in our list. Because of this, we can swap the value we want to remove with the value at the top of the list (we know where the value is due to our hashmap), and then just run `self.data.pop()` in constant time.

```python
class RandomizedSet:
	def __init__(self):
		# { val: index_of_val_in_data }
		self.map = {}
		self.data = []
	
	def insert(self, val: int) -> bool:
		if val in self.map:
			return False
	
		self.data.append(val)
		self.map[val] = len(self.data)-1
		return True
	
	
	def remove(self, val: int) -> bool:
		if val in self.map:
			if len(self.data) == 1:
				self.data = []
				self.map.clear()
				return True
	
			idx_of_val = self.map[val]
			last_element = self.data[-1]
		
			# update idx of last_element in map
			self.map[last_element] = idx_of_val
		
			# swap val and last_element
			self.data[-1], self.data[idx_of_val] = self.data[idx_of_val], self.data[-1]
		
			# remove val from map
			self.map.pop(val)
			# remove val from data
			self.data.pop()
	
			return True

		return False
```

### doubly-linked list w/ hashmap

I’m just going to leave this here because I managed to pass the test cases with this version, even though `getRandom` is technically $O(n)$. Maybe it’s because the insertion and deletion is fast with a DLL? Who knows, but probably don’t do this during an interview.

```python
class DLLNode:
	def __init__(self, val):
		self.val = val
		self.left = None
		self.right = None
  
class RandomizedSet:
	
	def __init__(self):
		self.head = DLLNode(None)
		self.tail = DLLNode(None)
		  
		self.head.left = None
		self.head.right = self.tail
		  
		self.tail.left = self.head
		self.tail.right = None
		  
		self.nodes = {}
	  
	def insert(self, val: int) -> bool:
		if val in self.nodes:
			return False
	  
		new_node = DLLNode(val)
		old_head_right = self.head.right
	  
		self.head.right = new_node
		new_node.right = old_head_right
		old_head_right.left = new_node
		new_node.left = self.head
		  
		self.nodes[val] = new_node
		return True
	  
	def remove(self, val: int) -> bool:
		if val not in self.nodes:
			return False
	  
		node_to_remove = self.nodes[val]
		node_to_remove.left.right = node_to_remove.right
		node_to_remove.right.left = node_to_remove.left
		  
		del self.nodes[val]
		return True
	
	def getRandom(self) -> int:
		vals = self.nodes.keys()
		return random.choice(list(vals))
```
