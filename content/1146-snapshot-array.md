---
type: leetcode
title: 1146. snapshot array
tags:
  - hashmap
  - binary-search
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-10-07
---

Implement a SnapshotArray that supports the following interface:

- `SnapshotArray(int length)` initializes an array-like data structure with the given length. **Initially, each element equals 0**.
- `void set(index, val)` sets the element at the given `index` to be equal to `val`.
- `int snap()` takes a snapshot of the array and returns the `snap_id`: the total number of times we called `snap()` minus `1`.
- `int get(index, snap_id)` returns the value at the given `index`, at the time we took the snapshot with the given `snap_id`

## solutions

First of all, the brute force solution is to copy the entire array whenever we snapshot, and just simply access the array at the snapshot for each `get` request. However, this makes `snapshot` $O(n)$, and the `get` call also $O(n)$.

Furthermore, the space complexity is $O(mn)$ where $m$ is the number of `snapshot` calls and $n$ is the length of the array.

### array w/ binary search on history

Borrowing some ideas from problems like [[362-design-hit-counter]] and [[981-time-based-key-value-store]], we realize that instead of storing the entire value of an array for each `snapshot`, we should only store a new copy when the value changes.

Then, if we map out each index in our array as a list of `(snapshot_id, value)` pairs, we can simply binary search for the biggest value that’s $\le$ `snapshot_id`.

This improves our space efficiency, and improves `get` requests to be $O(\log n)$ time. However, this solution times out because `snap` is still $O(n)$, as we store current values in a list of length $n$ and must iterate through the entire list to find changed values.

```python
class SnapshotArray:
	def __init__(self, length: int):
		# per index, sorted (snap, value) pairs
		self.arr = [0]*length
		self.snaps = None
		self.snap_id = 0

	def set(self, index: int, val: int) -> None:
		self.arr[index] = val
	
	def snap(self) -> int:
		# special case first snap
		if self.snap_id == 0:
			self.snaps = [[(0, val)] for val in self.arr]
		else:
			for i, snaps in enumerate(self.arr):
				if self.arr[i] != self.snaps[i][-1][1]:
					self.snaps[i].append((self.snap_id, self.arr[i]))
	
		self.snap_id += 1
		return self.snap_id-1
	
	def get(self, index: int, snap_id: int) -> int:
		# binary search for biggest snap_id <= snap request
		snaps = self.snaps[index]
		l, r = 0, len(snaps)
		while l <= r:
			m = (l+r)//2
	
			if snaps[m][0] <= snap_id and (
				m == len(snaps)-1 or snaps[m+1][0] > snap_id
			):
				return snaps[m][1]
			elif snaps[m][0] > snap_id:
				r = m-1
			else:
				l = m+1
```

### changeset w/ binary search on history

Instead of storing current values in a list, we can just keep a hashmap of changed indices, and their new values. We reset this whenever we write a new snapshot.

This improves the runtime of `snap` to the number of changes since the last snap, which is often much less than $n$.

```python
class SnapshotArray:
	
	def __init__(self, length: int):
		# per index, sorted (snap, value) pairs
		self.changeset = {}
		self.snaps = [[(0, 0)] for _ in range(length)]
		self.snap_id = 0
	  
	def set(self, index: int, val: int) -> None:
		self.changeset[index] = val
	  
	def snap(self) -> int:
		# special case first snap
		if self.snap_id == 0:
			for idx, val in self.changeset.items():
				self.snaps[idx][0] = (0, val)
		else:
			for idx, val in self.changeset.items():
				self.snaps[idx].append((self.snap_id, val))

		self.changeset.clear()
		self.snap_id += 1
		return self.snap_id-1
	  
	def get(self, index: int, snap_id: int) -> int:
		# binary search for biggest snap_id <= snap request
		snaps = self.snaps[index]
		l, r = 0, len(snaps)
		while l <= r:
			m = (l+r)//2
	
			if snaps[m][0] <= snap_id and (
				m == len(snaps)-1 or snaps[m+1][0] > snap_id
			):
				return snaps[m][1]
			elif snaps[m][0] > snap_id:
				r = m-1
			else:
				l = m+1
```
