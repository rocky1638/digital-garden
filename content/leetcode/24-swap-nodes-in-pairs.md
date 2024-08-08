---
title: 24. swap nodes in pairs
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/swap-nodes-in-pairs/
date: 2022-12-13
updated: 2024-08-03
tags:
  - linked-list
---

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

## solutions

### iterative

It’s the standard [[206-reverse-linked-list]] with two pointers, with some extra logic for only reversing groups of two.

```python
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return None
        if not head.next:
            return head

        dummy = ListNode(-1) 
        dummy.next = head

        # initialize the pointers on the nodes before the 
        # first ones that we need to swap
        left, right = dummy, head

        while left and left.next and right and right.next:
            right_of_right = right.next.next
            toswap_left = left.next
            toswap_right = right.next

            left.next = toswap_right
            toswap_right.next = toswap_left
            toswap_left.next = right_of_right

			# these swaps are not intuitive, just draw it out
            left = toswap_left
            right = right_of_right
        return dummy.next
```

### recursive (recommended)

Instead of complicating the reversal logic, we can just reverse the first two nodes, then recursively call the function on the rest of the list.

```python
def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
	if not head:
		return None
	if not head.next:
		return head

	n1, n2 = head, head.next
	  
	rest = n2.next
	n2.next = n1
	n1.next = self.swapPairs(rest)
	return n2
```
