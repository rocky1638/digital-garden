---
type: leetcode
title: 381. insert delete getrandom o(1) - duplicates allowed
tags: 
aliases: 
parents:
  - "[[380-insert-delete-getrandom-o(1)]]"
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-10-17
---

`RandomizedCollection` is a data structure that contains a collection of numbers, possibly duplicates (i.e., a multiset). It should support inserting and removing specific elements and also reporting a random element.

Implement the `RandomizedCollection` class:

- `RandomizedCollection()` Initializes the empty `RandomizedCollection` object.
- `bool insert(int val)` Inserts an item `val` into the multiset, even if the item is already present. Returns `true` if the item is not present, `false` otherwise.
- `bool remove(int val)` Removes an item `val` from the multiset if present. Returns `true` if the item is present, `false` otherwise. Note that if `val` has multiple occurrences in the multiset, we only remove one of them.
- `int getRandom()` Returns a random element from the current multiset of elements. The probability of each element being returned is **linearly related** to the number of the same values the multiset contains.

You must implement the functions of the class such that each function works on **average** `O(1)` time complexity.

**Note:** The test cases are generated such that `getRandom` will only be called if there is **at least one** item in the `RandomizedCollection`.

## solution

Very similar to [[380-insert-delete-getrandom-o(1)]], but we keep a set of all the indices where a value exists instead of just a single number.

Note that when we delete, we don’t care which one we delete, so an unordered set works perfectly fine here.

```python
class RandomizedCollection:
	def __init__(self):
		self.a = []
		self.idx = defaultdict(set)
	  
	def insert(self, val: int) -> bool:
		self.idx[val].add(len(self.a))
		self.a.append(val)
		return len(self.idx[val]) == 1
	  
	def remove(self, val: int) -> bool:
		if not self.idx[val]:
			return False
		to_remove, last = self.idx[val].pop(), self.a[-1]
		# copy value at end into index that contains val
		self.a[to_remove] = last
		self.idx[last].add(to_remove)
		self.idx[last].remove(len(self.a)-1)
		  
		self.a.pop()
		return True
	  
	def getRandom(self) -> int:
		return random.choice(self.a)
```
