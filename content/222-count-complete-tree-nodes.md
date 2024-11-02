---
type: leetcode
title: 222. count complete tree nodes
tags:
  - binary-tree
  - binary-search
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-13
updated: 2024-11-02
---

Given the `root` of a **complete** binary tree, return the number of the nodes in the tree.

According to **[Wikipedia](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)**, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between `1` and `2h` nodes inclusive at the last level `h`.

Design an algorithm that runs in less than `O(n)` time complexity.

## solution

Given that we must give a better the $O(n)$ solution, a simple traversal is not allowed here. Instead, we can first find the height of the tree, and then figure out how many nodes are missing from the final layer.

We can figure out the number of missing nodes in the tree by binary searching it. The tricky part is figuring out how to binary search the last layer by traversing the tree.

Basically, we know we have some nodes in the index range $[0, n-1]$ where $n=2^{h-1}$ where $h$ is the height of the tree. We binary search, and given the index we’re searching for, if the value is in the left half of the range, we can go to `node.left`, and if the value is in the right range, we can go to `node.right`. Note that we must update our target, as we’ve moved the base of our index/offset.

```python
def findHeight(self, root):
	height = 0
	cur = root
	while cur:
		cur = cur.left
		height += 1
	return height

# note that total is always a power of 2
def exists(self, target, root, total):
	# base case
	if total == 2:
		if target == 0 and root.left:
			return True
		elif target == 1 and root.right:
			return True
	return False
  
	# if the idx we're searching for is less than half of search space,
	# we go left
	if target < total/2:
		return self.exists(target, root.left, total/2)
	# else, remove total/2 from idx and go right
	else:
		return self.exists(target-total/2, root.right, total/2)

# O(log^2(n))
def countNodes(self, root: Optional[TreeNode]) -> int:
	height = self.findHeight(root)
	if height == 0:
		return 0
	if height == 1:
		return 1
  
	# there are between 1 and 2^(h-1) nodes
	# in the last incomplete level
	total = 2**(height-1)
	lo, hi = 0, total-1
	  
	# binary search for the first missing node
	while lo <= hi:
		mid = (lo+hi)//2
		if self.exists(mid, root, total) and (mid == total or not self.exists(mid+1, root, total)):
			return 2**(height-1)+mid
		elif self.exists(mid, root, total):
			lo = mid+1
		else:
			hi = mid-1
	# handle fully complete tree
	return 2**(height)-1
```
