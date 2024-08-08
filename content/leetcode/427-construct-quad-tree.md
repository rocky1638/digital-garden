---
type: leetcode
title: 427. construct quad tree
tags:
  - recursion
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-06
updated: 2024-08-06
---

Given a `n * n` matrix `grid` of `0's` and `1's` only. We want to represent `grid` with a Quad-Tree.

Return _the root of the Quad-Tree representing_ `grid`.

A Quad-Tree is a tree data structure in which each internal node has exactly four children. Besides, each node has two attributes:

- `val`: True if the node represents a grid of 1's or False if the node represents a grid of 0's. Notice that you can assign the `val` to True or False when `isLeaf` is False, and both are accepted in the answer.
- `isLeaf`: True if the node is a leaf node on the tree or False if the node has four children.

class Node {
    public boolean val;
    public boolean isLeaf;
    public Node topLeft;
    public Node topRight;
    public Node bottomLeft;
    public Node bottomRight;
}

We can construct a Quad-Tree from a two-dimensional area using the following steps:

1. If the current grid has the same value (i.e all `1's` or all `0's`) set `isLeaf` True and set `val` to the value of the grid and set the four children to Null and stop.
2. If the current grid has different values, set `isLeaf` to False and set `val` to any value and divide the current grid into four sub-grids as shown in the photo.
3. Recurse for each of the children with the proper sub-grid.

![](https://assets.leetcode.com/uploads/2020/02/11/new_top.png)

If you want to know more about the Quad-Tree, you can refer to the [wiki](https://en.wikipedia.org/wiki/Quadtree).

## solutions

### basic recursion

We first check to see if the current square should be a leaf node. If not, we recurse on the four quadrants.

The repeated work here is that if we do end up needing to recurse, we have to iterate over the same squares again. This gives a time complexity of $O(N^2 \log N)$.

![[427-construct-quad-tree-time-complexity.png]]

```python
def construct(self, grid: List[List[int]]) -> 'Node':
	m, n = len(grid), len(grid[0])
	  
	def recurse(x1, y1, x2, y2):
		seen = set()
		for i in range(x1, x2+1):
			for j in range(y1, y2+1):
				seen.add(grid[i][j])

		# base case
		if len(seen) == 1:
			val = seen.pop()
			return Node(val=val, isLeaf=True)
	  
		midX = (x1 + x2) // 2
		midY = (y1 + y2) // 2
		  
		topLeft = recurse(x1, y1, midX, midY)
		topRight = recurse(x1, midY + 1, midX, y2)
		bottomLeft = recurse(midX + 1, y1, x2, midY)
		bottomRight = recurse(midX + 1, midY + 1, x2, y2)
		  
		return Node(
			val=None,
			isLeaf=False,
			topLeft=topLeft,
			topRight=topRight,
			bottomLeft=bottomLeft,
			bottomRight=bottomRight
		)
	return recurse(0,0,m-1,n-1)
```

### optimized recursion

Instead of checking if a square is a leaf node at every level, let’s just recurse all the way to the root first, and then when we come back up, we’ll only ever need to check the four children.

This way, we only ever look at each cell once, and so our runtime is $O(N^2)$.

```python
def construct(self, grid: List[List[int]]) -> 'Node':
	n = len(grid)
	  
	def recurse(x1, y1, x2, y2):
		if x1 == x2 and y1 == y2:
			return Node(val=grid[x1][y1], isLeaf=True)

		midX = (x1 + x2) // 2
		midY = (y1 + y2) // 2
		  
		tl = recurse(x1, y1, midX, midY)
		tr = recurse(x1, midY + 1, midX, y2)
		bl = recurse(midX + 1, y1, x2, midY)
		br = recurse(midX + 1, midY + 1, x2, y2)
		  
		if (
			tl.isLeaf
			and tr.isLeaf
			and bl.isLeaf
			and br.isLeaf
		):
			if tl.val == tr.val == bl.val == br.val:
				return Node(val=tl.val, isLeaf=True)
		  
		return Node(
			val=None,
			isLeaf=False,
			topLeft=tl,
			topRight=tr,
			bottomLeft=bl,
			bottomRight=br
		)
	return recurse(0,0,n-1,n-1)
```
