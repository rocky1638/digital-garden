---
type: leetcode
title: 314. binary tree vertical order traversal
date: 2022-11-29
updated: 2024-07-10
tags:
  - bfs
  - hashmap
---

Given the `root` of a binary tree, return _**the vertical order traversal** of its nodes' values_. (i.e., from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from **left to right**.

## solutions

### bfs with sorting

We keep a hashmap that tracks the vertical columns of nodes. We also keep track of column index as we bfs, where the root node has a column of 0.

```python
class Solution:
    def verticalOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return None
        
        # root is at column 0, left child -1, right child +1
        columns = defaultdict(list)
        ans = []
        
        # q[i] = (node, column_idx)
        q = deque([(root, 0)])
        
        # level order traversal with bfs
        while q:
            cur, col = q.popleft()
            columns[col].append(cur.val)
            
            if cur.left: q.append((cur.left, col-1))
            if cur.right: q.append((cur.right, col+1))
        
        for key in sorted(list(columns.keys())):
            ans.append(columns[key])
        return ans
            
```

### bfs without sorting

Instead of sorting, we can keep track of the column values and the minimum column we’ve seen, and then use that to just create an output array of set length and use the minimum column as an offset to index into this output array.

```python
def verticalOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
	if not root:
		return []
	  
	cols = defaultdict(list)
	q = deque([(root, 0)])
	col_values = set()
	min_col = 0
	  
	while q:
		node, col = q.popleft()

		cols[col].append(node.val)
		col_values.add(col)
		min_col = min(min_col, col)
	  
		if node.left: q.append((node.left, col-1))
		if node.right: q.append((node.right, col+1))

	ans = [[] for _ in range(len(col_values))]
	for key in cols:
		shifted_key = key - min_col
		ans[shifted_key] = cols[key]
	return ans
```
