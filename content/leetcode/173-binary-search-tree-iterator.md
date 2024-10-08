---
type: leetcode
title: 173. binary search tree iterator
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-01
updated: 2024-09-01
---

Implement the `BSTIterator` class that represents an iterator over the **[in-order traversal](https://en.wikipedia.org/wiki/Tree_traversal#In-order_(LNR))** of a binary search tree (BST):

- `BSTIterator(TreeNode root)` Initializes an object of the `BSTIterator` class. The `root` of the BST is given as part of the constructor. The pointer should be initialized to a non-existent number smaller than any element in the BST.
- `boolean hasNext()` Returns `true` if there exists a number in the traversal to the right of the pointer, otherwise returns `false`.
- `int next()` Moves the pointer to the right, then returns the number at the pointer.

Notice that by initializing the pointer to a non-existent smallest number, the first call to `next()` will return the smallest element in the BST.

You may assume that `next()` calls will always be valid. That is, there will be at least a next number in the in-order traversal when `next()` is called.

## solutions

### recursive inorder traversal

Just do a recursive inorder traversal and save the list.

```python
class BSTIterator:
	def __init__(self, root: Optional[TreeNode]):
		self.arr = [None]
		self.idx = 0
		self._to_list(root)
	  
	def _to_list(self, node):
		if not node:
			return
	  
		self._to_list(node.left)
		self.arr.append(node.val)
		self._to_list(node.right)
	  
	def next(self) -> int:
		self.idx += 1
		return self.arr[self.idx]
	  
	def hasNext(self) -> bool:
		return self.idx < len(self.arr)-1
```
