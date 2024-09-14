---
type: leetcode
title: 113. path sum ii
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/path-sum-ii/
date: 2022-12-13
updated: 2024-09-02
---

Given the `root` of a binary tree and an integer `targetSum`, return _all **root-to-leaf** paths where the sum of the node values in the path equals_ `targetSum`_. Each path should be returned as a list of the node **values**, not node references_.

A **root-to-leaf** path is a path starting from the root and ending at any leaf node. A **leaf** is a node with no children.

## solution

- simple [[dfs]] with [[recursion]] on the [[binary-tree]].
- keep an accumulator [[array]], if we reach a leaf and have the correct path sum, add it to the output array.

```python
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        if not root:
            return []

        ans = []
        acc = [root.val]
        tally = root.val

        def recurse(node):
            nonlocal ans
            nonlocal tally
            
            if not node.left and not node.right:
                if tally == targetSum:
                    ans.append(acc[:])
            else:
                if node.left:
                    acc.append(node.left.val)
                    tally += node.left.val
                    recurse(node.left)
                    tally -= node.left.val
                    acc.pop()
                if node.right:
                    acc.append(node.right.val)
                    tally += node.right.val
                    recurse(node.right)
                    tally -= node.right.val
                    acc.pop()

        recurse(root)
		return ans
```

As a mild improvement, we don’t need to backtrack between the left and right calls.

```python
def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
	res = []
	path = []
	acc = 0
	  
	def recurse(node):
		nonlocal acc, path
		if not node:
			return

		# add current node
		path.append(node.val)
		acc += node.val

		# leaf base case
		if not node.left and not node.right:
			if acc == targetSum:
				res.append(path[:])
		else:
			recurse(node.left)
			recurse(node.right)

		# backtrack
		acc -= node.val
		path.pop()

	recurse(root)
	return res
```

Categories:: [[dfs]], [[recursion]], [[binary-tree]], [[tree]], [[array]]
