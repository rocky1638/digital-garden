---
type: leetcode
title: 437. path sum iii
tags:
  - prefix-sums
  - binary-tree
  - dfs
date: 2022-12-29
updated: 2024-09-10
---

Given the `root` of a binary tree and an integer `targetSum`, return _the number of paths where the sum of the values along the path equals_ `targetSum`.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

![[437-path-sum-iii.png]]

## solutions

### nested recursion starting from every node

Each call of `recurse` finds all the paths starting at `node`. In the main function, we try calling `recurse` with every node.

```python
def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
	if not root:
		return 0

	ans = 0
	acc = 0

	def recurse(node):
		nonlocal acc, ans
		if not node:
			return
	
		acc += node.val
		if acc == targetSum:
			ans += 1
	
		recurse(node.left)
		recurse(node.right)

		# backtrack
		acc -= node.val

	# all paths starting at root
	recurse(root) 
	# all paths starting at children
	ans += self.pathSum(root.left, targetSum)
	ans += self.pathSum(root.right, targetSum)
	return ans 
```

### recursion + prefix sums

We basically do the idea of [[523-continuous-subarray-sum]] or [[525-contiguous-array]]. We keep a count of the number of times each prefix appears, and then we can calculate how many paths ending at the current node sum to `targetSum` in constant time.

```python
def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
	ans = 0
	prefix_counts = Counter()
	prefix_counts[0] = 1
	acc = 0
	
	def recurse(node):
		nonlocal acc, ans
		if not node:
			return

		acc += node.val
		ans += prefix_counts[acc-targetSum]
	
		prefix_counts[acc] += 1
		recurse(node.left)

		recurse(node.right)

		# backtrack
		prefix_counts[acc] -= 1
		acc -= node.val
	
	recurse(root)
	return ans
```
