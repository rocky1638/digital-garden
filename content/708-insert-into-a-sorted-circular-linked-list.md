---
type: leetcode
title: 708. insert into a sorted circular linked list
tags:
  - linked-list
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-02
updated: 2024-09-02
---

Given a Circular Linked List node, which is sorted in non-descending order, write a function to insert a value `insertVal` into the list such that it remains a sorted circular list. The given node can be a reference to any single node in the list and may not necessarily be the smallest value in the circular list.

If there are multiple suitable places for insertion, you may choose any place to insert the new value. After the insertion, the circular list should remain sorted.

If the list is empty (i.e., the given node is `null`), you should create a new single circular list and return the reference to that single node. Otherwise, you should return the originally given node.

## solution

Implement it with one or two pointers, but be mindful of some edge cases.

```python
def insert(self, head: 'Optional[Node]', insertVal: int) -> 'Node':
	new_node = Node(insertVal)
	  
	if not head:
		new_node.next = new_node
		return new_node

	if head.next == head:
		head.next = new_node
		new_node.next = head
		return head
	  
	cur = head
	to_insert = False
	while True:
		# we can insert (break cases) #
		# normal insertion into middle
		if cur.val <= insertVal and cur.next.val >= insertVal:
			to_insert = True
		# head is on last node before cycle
		elif (
			cur.val > cur.next.val
			and (insertVal >= cur.val or insertVal <= cur.next.val)
		):
			to_insert = True
	  
		# else, move forward
		else:
			cur = cur.next
			# if we've iterated whole list and found no spot,
			# that means list is monotone. Just insert anywhere
			if cur == head:
			to_insert = True
	  
		if to_insert:
			new_node.next = cur.next
			cur.next = new_node
			return head
```
