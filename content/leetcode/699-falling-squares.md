---
type: leetcode
title: 699. falling squares
tags:
  - segment-tree
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-18
updated: 2024-08-18
---

There are several squares being dropped onto the X-axis of a 2D plane.

You are given a 2D integer array `positions` where `positions[i] = [lefti, sideLengthi]` represents the `ith` square with a side length of `sideLengthi` that is dropped with its left edge aligned with X-coordinate `lefti`.

Each square is dropped one at a time from a height above any landed squares. It then falls downward (negative Y direction) until it either lands **on the top side of another square** or **on the X-axis**. A square brushing the left/right side of another square does not count as landing on it. Once it lands, it freezes in place and cannot be moved.

After each square is dropped, you must record the **height of the current tallest stack of squares**.

Return _an integer array_ `ans` _where_ `ans[i]` _represents the height described above after dropping the_ `ith` _square_.

## solutions

### logical solution

The key thing to realize here is “what queries will this square affect in the future?”. And the answer to that is any future squares that will overlap with this square!

So we iterate through the squares, and after updating the value of the current query, we check if any future queries will be affected by this square. If so, we update those future values as well, because we know when we reach that future query, it will at minimum be the current height + the size of the new square.

Then, to answer, we just propagate a monotonically increasing value through our queries array to satisfy the output, which is the global maximum after each square.

```python
def fallingSquares(self, positions: List[List[int]]) -> List[int]:
	queries = [0]*len(positions)
	for i, (left, size) in enumerate(positions):
		right = left + size
		queries[i] += size
		  
		for j in range(i+1, len(positions)):
			left2, size2 = positions[j]
			right2 = left2 + size2
	  
			if left2 < right and left < right2:
				queries[j] = max(queries[j], queries[i])

	ans = [-inf]
	for val in queries:
		ans.append(max(val, ans[-1]))
	return ans[1:]
```

### segment tree

The above solution is $O(n^2)$, but we can improve the solution to $O(n\log n)$ with segment trees. It’s pretty easy to notice that we are looking to query and update ranges of values, and so segment trees lend themselves nicely to this use case.


> [!info]+ An explanation of coordinate compression
> Coordinate compression allows us to map a bunch of coordinates in a sparse range into a contiguous length of only the coordinates that we care about.
>
> 1. **Collect All Relevant Coordinates:**
>
> First, gather all the unique X-coordinates that you will be working with. In your problem, for each square's left position `left` and the position `left + sideLength` (i.e., the right edge), these positions are relevant.
>
> For example, if your positions are [(4, 4), (1, 3), (7, 2)], you need the start (`left`) and end (`left + sideLength`) points:
>
> From the above, relevant coordinates are: 1, 4, 8, 7, 9.
>
> 2. **Sort the Coordinates:**
>
> Sort the collected coordinates to determine their relative order.
> For the example above, sorting gives: [1, 4, 7, 8, 9].
>
> 3. **Map Coordinates to Compressed Values:**
>
> Create a mapping from each original coordinate to its index in the sorted list. This index represents the compressed coordinate.
>
> For example, in the sorted list [1, 4, 7, 8, 9], the mapping would be:
>
> 1 -> 0
> 4 -> 1
> 7 -> 2
> 8 -> 3
> 9 -> 4
>
> Now, instead of using the original coordinates, you use the compressed coordinates (indices) in your segment tree or other data structure.

```python
class SegmentTreeNode:
	def __init__(self, low, high):
		self.low = low
		self.high = high
		self.left = None
		self.right = None
		self.max = 0
  
class Solution:
	def _build(self, left, right):
		root = SegmentTreeNode(self.coords[left], self.coords[right])
		if left == right:
			return root
		mid = (left+right)//2
		root.left = self._build(left, mid)
		root.right = self._build(mid+1, right)
		return root

	def _update(self, root, lower, upper, val):
		if not root:
			return
		# intersect (if no intersect, do nothing)
		if lower <= root.high and root.low <= upper:
			root.max = val
			self._update(root.left, lower, upper, val)
			self._update(root.right, lower, upper, val)

	def _query(self, root, lower, upper):
		# fully covers, outer edges of query handled by other nodes
		if lower <= root.low and root.high <= upper:
			return root.max
		# disjoint
		if upper < root.low or root.high < lower:
			return 0
		# intersection
		return max(
			self._query(root.left, lower, upper),
			self._query(root.right, lower, upper)
		)

	def fallingSquares(self, positions: List[List[int]]) -> List[int]:
		# coordinates compression
		coords = set()
		for left, size in positions:
			right = left+size-1
			coords.add(left)
			coords.add(right)
		self.coords = sorted(list(coords))
		root = self._build(0, len(self.coords)-1)

		res = []
		for left, size in positions:
			right = left+size-1
			# get current max height of range
			h = self._query(root, left, right) + size
			# append global maximum to res
			res.append(max(res[-1], h)) if res else res.append(h)
			# update height of range of new square
			self._update(root, left, right, h)
		return res
```

## references

- https://stackoverflow.com/questions/3269434/whats-the-most-efficient-way-to-test-if-two-ranges-overlap
