---
type: leetcode
title: 297. serialize and deserialize binary tree
date: 2022-11-24
updated: 2024-08-25
tags:
  - dfs
  - binary-tree
---

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

```python
class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        # in order traversal, use a null for any node that's
        # not there, just like leetcode
        a = []
        
        def dfs(node):
            if node:
                a.append(str(node.val))
                dfs(node.left)
                dfs(node.right)
            else:
                a.append("null")

        dfs(root)
        return ",".join(a)
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        # add a 0 so that nodes are 1-indexed
        # that way, children for node at i are at 2i and 2i+1
        if len(data) == 0:
            return None
        a = data.split(",")
        a = deque(a)
        
        def recurse():
            if a[0] == "null":
                a.popleft()
                return None
            else:
                node = TreeNode(a[0])
                a.popleft()
                node.left = recurse()
                node.right = recurse()
                return node
        
        return recurse()
```

- i just do a preorder traversal of the [[binary-tree]] and append `null` to the string when we reach a null node in our traversal.
- for the deserialization, we can similarly go recursively, just popping nodes/nones off the front of our array.

[[dfs]], [[tree]], [[string]]
