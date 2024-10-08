---
type: leetcode
title: 307. range sum query - mutable
tags:
  - segment-tree
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-09-06
---

Given an integer array `nums`, handle multiple queries of the following types:

1. **Update** the value of an element in `nums`.
2. Calculate the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** where `left <= right`.

Implement the `NumArray` class:

- `NumArray(int[] nums)` Initializes the object with the integer array `nums`.
- `void update(int index, int val)` **Updates** the value of `nums[index]` to be `val`.
- `int sumRange(int left, int right)` Returns the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** (i.e. `nums[left] + nums[left + 1] + ... + nums[right]`).

## solutions

```python
class SegmentNode:
    def __init__(self, lower, upper):
        self.lower = lower
        self.upper = upper
        self.left = None
        self.right = None
        self.sum = 0

    def __str__(self):
        return f"SegmentNode(lower={self.lower}, upper={self.upper}, sum={self.sum}"

    def query(self, l, r):
        # we take the full range of this node
        if l <= self.lower and r >= self.upper:
            return self.sum
        # we take none (disjoint)
        if r < self.lower or l > self.upper:
            return 0
        # partial intersection
        else:
            return self.left.query(l, r) + self.right.query(l, r)
    
    def update(self, idx, delta):
        if self.lower <= idx <= self.upper:
            self.sum += delta

            if self.left:
                self.left.update(idx, delta)
            if self.right:
                self.right.update(idx, delta)

class NumArray:
    def __init__(self, nums: List[int]):
        self.root = self.build_tree(nums, 0, len(nums)-1)
        self.nums = nums

    def print_tree(self):
        q = deque([self.root])
        while q:
            level_len = len(q)

            for _ in range(level_len):
                cur = q.popleft()
                print(cur, end=", ")
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
            print("\n----")
    
    def build_tree(self, nums, l, r):
        node = SegmentNode(l, r)
        if l == r:
            node.sum = nums[l] 
        else:
            m = (l+r)//2
            left = self.build_tree(nums, l, m)
            right = self.build_tree(nums, m+1, r)
            node.sum = left.sum+right.sum
            node.left = left
            node.right = right
        return node

    def update(self, index: int, val: int) -> None:
        delta = val - self.nums[index]

        if delta != 0:
            self.nums[index] = val
            self.root.update(index, delta)

    def sumRange(self, left: int, right: int) -> int:
        return self.root.query(left, right)

```
