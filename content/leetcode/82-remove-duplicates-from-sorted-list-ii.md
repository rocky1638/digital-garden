---
type: leetcode
title: 82. remove duplicates from sorted list ii
tags:
  - linked-list
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-21
updated: 2024-09-21
---

Given the `head` of a sorted linked list, _delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list_. Return _the linked list **sorted** as well_.

## solution

Iterate through the whole block before deciding to add or remove the value (use a helper function).

```python
def deleteDuplicates(self, head: Optional[ListNode]):
	dummy = ListNode()
	prev, cur = dummy, head
	  
	def traverse_block(node):
		prev = node.val
		length = 0
		while node and node.val == prev:
			node = node.next
			length += 1
		return length, node
	  
	while cur:
		length, nex = traverse_block(cur)
		# take the value
		if length == 1:
			prev.next = cur
			prev = cur
			cur = cur.next
		else: # skip the block
			cur = nex
			prev.next = None
	  
	return dummy.next
```
