---
title: 124. binary tree maximum path sum
type: leetcode
aliases: 
difficulty: 🔴
link: https://leetcode.com/problems/binary-tree-maximum-path-sum/
date: 2022-12-12
updated: 2024-03-27
tags:
  - binary-tree
---

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

## solution

Use a fancy recursion method on the binary tree. At each recursive step, we return the maximum possible path either passing through the current node, or just overall in the subtree.


> [!attention]
>
> Note that we can’t include the value of `node.val + lmi + rmi` in the check for `max_including` because if we end up using both children, then we can’t connect to a parent node, because that would require passing through one of the edges to the child nodes twice in order to get back up the tree.

```python
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        def recurse(node):
            """
            for each binary tree with root node, we can have a maximum path in several ways:
                - maximum path of left subtree, not including node 
                - maximum path of right subtree, not including node
                - maximum path of left subtree, including node
                - maximum path of right subtree, including node
                - maximum path of both subtrees and connecting with node
				
            we have all these options because one side could be all
            negative numbers, causing us to not want to include them.

            so, at each node, we should return the maximum path including
            the node, and overall regardless.
			
            return (max including, max overall)
            """

            # base case
            if not node:
                return float("-inf"), float("-inf")

            lmi, lmo = recurse(node.left)
            rmi, rmo = recurse(node.right)

            max_including = max(
                node.val,
                node.val + lmi,
                node.val + rmi,
            ) 

            max_overall = max(
                max_including,
                node.val + lmi + rmi,
                lmo,
                rmo,
            )

            return max_including, max_overall

        return recurse(root)[1]
```
