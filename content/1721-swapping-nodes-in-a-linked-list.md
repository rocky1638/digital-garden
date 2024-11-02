---
type: leetcode
title: 1721. swapping nodes in a linked list
tags:
  - linked-list
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-23
updated: 2024-10-23
---

You are given the `head` of a linked list, and an integer `k`.

Return _the head of the linked list after **swapping** the values of the_ `kth` _node from the beginning and the_ `kth` _node from the end (the list is **1-indexed**)._

![[1721-swapping-nodes-in-a-linked-list.png]]

## solutions

### swapping values

This is what they ask for, and is pretty straightforward with a slow and fast pointer approach.

```python
def swapNodes(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
	# find kth node and prev of it
	# find kth node from end and prev of it
	  
	if not head.next:
		return head
	  
	fast = head
	# find node k
	for _ in range(k-1):
		fast = fast.next
	c1 = fast
	  
	slow = head # slow on head (1)
	while fast.next:
		slow = slow.next
		fast = fast.next
	c2 = slow
	  
	c1.val, c2.val = c2.val, c1.val
	return head
```

### actually swapping

If instead we need to actually swap the nodes, we can make use of a `dummy` node to avoid some edge cases, and also store the respective previous nodes for each node we’re swapping.

Note that we need to handle the edge cases where the two nodes are adjacent.

```python
def swapNodes(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
	# find kth node and prev of it
	# find kth node from end and prev of it
	dummy = ListNode()
	dummy.next = head
	  
	slow = fast = c1 = c2 = p1 = p2 = dummy
	  
	# find kth node and prev of it
	for _ in range(k):
	p1 = fast
		fast = fast.next
	c1 = fast
	  
	# find kth from end and prev
	while fast:
	p2 = slow
		fast = fast.next
		slow = slow.next
	c2 = slow
	  
	# adjacent edge cases
	if c1.next == c2:
		p1.next = c2
		c1.next = c2.next
		c2.next = c1
	elif c2.next == c1:
		p2.next = c1
		c2.next = c1.next
		c1.next = c2

	else:
		n1, n2 = c1.next, c2.next
	  
		p1.next = c2
		c2.next = n1
		  
		p2.next = c1
		c1.next = n2
	return dummy.next
```
