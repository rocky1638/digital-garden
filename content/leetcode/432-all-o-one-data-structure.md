---
type: leetcode
title: 432. all o(1) data structure
tags:
  - linked-list
  - hashmap
aliases: 
parents: 
children: 
supports:
  - "[[146-lru-cache]]"
enemies: 
date: 2024-08-10
updated: 2024-08-10
---

Design a data structure to store the strings' count with the ability to return the strings with minimum and maximum counts.

Implement the `AllOne` class:

- `AllOne()` Initializes the object of the data structure.
- `inc(String key)` Increments the count of the string `key` by `1`. If `key` does not exist in the data structure, insert it with count `1`.
- `dec(String key)` Decrements the count of the string `key` by `1`. If the count of `key` is `0` after the decrement, remove it from the data structure. It is guaranteed that `key` exists in the data structure before the decrement.
- `getMaxKey()` Returns one of the keys with the maximal count. If no element exists, return an empty string `""`.
- `getMinKey()` Returns one of the keys with the minimum count. If no element exists, return an empty string `""`.

**Note** that each function must run in `O(1)` average time complexity.

## solution

Use a doubly-linked-list with two hashmaps, to allow for $O(1)$ of all operations. It’s quite similar to the [[146-lru-cache]] problem, but instead of using a node for each value, we use a node for each frequency (like a bucket per frequency), and then maintain sorted order of the nodes.

Also, we make sure that the nodes at head and tail are always non-empty, represent the minimum and maximum frequencies, so we can solve `getMaxKey` and `getMinKey` in $O(1)$.

During `inc` and `dec` steps, we have to make sure to remove nodes from the min and max positions of the DLL if they become empty.

Highly recommend writing out the main logic while delegating work to helper functions on a `DLL` or `DLLNode` class, so you don’t get bogged down in nitty-gritty implementation details. Use a sentinel `head` and `tail` node to simplify insertion and deletion logic of the linked list.
