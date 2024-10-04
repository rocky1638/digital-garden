---
type: leetcode
title: 25. reverse nodes in k-group
tags:
  - recursion
  - linked-list
aliases: 
difficulty: 🔴
link: https://leetcode.com/problems/reverse-nodes-in-k-group/
date: 2023-01-08
updated: 2024-09-21
parents:
  - "[[206-reverse-linked-list]]"
---

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.
You may not alter the values in the list's nodes, only nodes themselves may be changed.

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

## solutions

### recursion

- we reverse the first `k` nodes if they exist, and then connect the tail of this reversed list to the result of the recursive call on the rest of the list.
	- because of the recursion, we return the head of the entire list at the end of the recursive function.

```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev, cur = None, head
        tail = head
        
        while cur:
            nex = cur.next
            cur.next = prev
            prev = cur
            cur = nex
        
        return prev, tail

    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        """
        - reverse the first k elements
        - return the head of the reversed list linked
          to the recursive of the rest of list
        """
        if not head:
            return None

        # find kth node
        cur = head
        # if k is 1, we want to end on the head node
        for _ in range(k-1):
            if cur:
                cur = cur.next
            else: break
        
        rest = None
        # store rest of list's head
        if cur:
            rest = cur.next

            # disconnect rest of list
            cur.next = None

            # reverse the list
            reversed_head, reversed_tail = self.reverseList(head)

            # link tail to rest of list
            reversed_tail.next = self.reverseKGroup(rest, k)
            
            return reversed_head

        else:
            return head
```

### iterative

This is less intuitive, but essentially we need to keep track of our previous tail (which starts at `dummy`), and return the head of the new reversed portion + the next head to reverse from `reverse()`.

Remember to attach the last piece (unreversed) before returning!

```python
def reverseKGroup(self, head: Optional[ListNode], k: int):
	# determine length
	n, curr = 0, head
	while curr:
		n += 1
		curr = curr.next
	
	def reverse(node):
		prev, cur = None, node
	
		for _ in range(k):
			nex = cur.next
			cur.next = prev
			prev = cur
			cur = nex
		# prev is rev_head, cur is next piece to access
		return prev, cur
	
	# dummy -> first_k -> next_k
	dummy = prev_tail = ListNode()
	cur = head

	# by doing this, we don't need
	# to count nodes for every reversal
	for _ in range(n//k):
		rev_head, next_head = reverse(cur)
		prev_tail.next = rev_head
		# cur is now sitting at tail of just reversed k-list
		prev_tail = cur
		cur = next_head
	
	# connect up last sub-length-k list 
	prev_tail.next = cur
	return dummy.next 
```
