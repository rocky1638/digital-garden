---
type: leetcode
title: 138. copy list with random pointer
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/copy-list-with-random-pointer/
date: 2023-01-07
updated: 2024-08-29
tags:
  - linked-list
  - hashmap
---

A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return _the head of the copied linked list_.

The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

- `val`: an integer representing `Node.val`
- `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.

Your code will **only** be given the `head` of the original linked list.

## solution

We keep a hash table that maps the old nodes to the new nodes. Optionally, we can use the `id()` function to key by the memory addresses of the old nodes.

```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head: return None

        cur = head
        prev = None
        h = {}

        # create copies of all the nodes
        while cur:
            # create copy and save in hashmap
            copy = Node(cur.val)
            h[id(cur)] = copy

            # set next pointer of previous node
            if prev:
                h[id(prev)].next = copy
            
            # increment index and cur pointer
            prev = cur
            cur = cur.next
        
        cur = head
        while cur:
            # set random pointer on copied nodes
            # based on old nodes
            if cur.random:
                h[id(cur)].random = h[id(cur.random)]
            cur = cur.next
        
        return h[id(head)]
```

Here’s another solution in one-pass, where we just create copies for future nodes on a per-need basis.

```python
def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
	if not head:
		return head

	d = {}
	cur = head
	  
	while cur:
		# get_or_create cur copy
		if cur not in d:
			d[cur] = Node(cur.val)
		cur_copy = d[cur]
	  
		# set and create next copy if necessary
		if cur.next:
			if cur.next not in d:
				d[cur.next] = Node(cur.next.val)
			cur_copy.next = d[cur.next]

		# set and create random copy if necessary
		if cur.random:
			if cur.random not in d:
				d[cur.random] = Node(cur.random.val)
			cur_copy.random = d[cur.random]

		cur = cur.next
	return d[head]
```
