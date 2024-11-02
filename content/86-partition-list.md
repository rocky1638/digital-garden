---
type: leetcode
title: 86. partition list
tags:
  - linked-list
  - two-pointer
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-17
updated: 2024-10-17
---

Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

![[86-partition-list.png]]

## solution

Once you visualize this one, it’s pretty self-explanatory. We construct two linked lists for the left and right half as we iterate through it with a `cur` pointer. Connect them up at the end.

```python
def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
	if not head or not head.next:
		return head
	  
	left_dummy = ListNode()
	right_dummy = ListNode()
	  
	cur = head
	lc, rc = left_dummy, right_dummy
	  
	while cur:
		if cur.val < x:
			lc.next = cur
			lc = lc.next
		else:
			rc.next = cur
			rc = rc.next
		cur = cur.next

	lc.next = right_dummy.next
	rc.next = None
	  
	return left_dummy.next
```
