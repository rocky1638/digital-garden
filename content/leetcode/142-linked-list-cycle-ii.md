---
type: leetcode
title: 142. linked list cycle ii
tags:
  - linked-list
aliases: 
parents:
  - "[[141-linked-list-cycle]]"
children: 
supports: 
enemies: 
date: 2024-10-03
updated: 2024-10-03
---

Given the `head` of a linked list, return _the node where the cycle begins. If there is no cycle, return_ `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to (**0-indexed**). It is `-1` if there is no cycle. **Note that** `pos` **is not passed as a parameter**.

**Do not modify** the linked list.

## solution

Use Floyd’s algorithm, but then move one of the nodes back to the front and move in lockstep.

```python
def detectCycle(self, head: Optional[ListNode]):  
	# edge case for 0 and 1 node lists  
	if not head or not head.next:  
		return None  
	
	# floyd's algo  
	slow, fast = head, head  
	while fast and fast.next:  
		slow = slow.next  
		fast = fast.next.next  
	
	if slow == fast:  
		break  
	
	# if we broke before meeting, no cycle exists   
	if slow != fast:  
		return None  
	
	# reset slow to head and move lockstep  
	slow = head  
	while slow != fast:  
		slow = slow.next  
		fast = fast.next  
	
	return slow
```
