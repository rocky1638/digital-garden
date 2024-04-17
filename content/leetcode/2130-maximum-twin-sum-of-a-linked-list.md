---
type: leetcode
title: 2139. maximum twin sum of a linked list
tags:
  - linked-list
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-03-30
---

In a linked list of size `n`, where `n` is **even**, the `ith` node (**0-indexed**) of the linked list is known as the **twin** of the `(n-1-i)th` node, if `0 <= i <= (n / 2) - 1`.

- For example, if `n = 4`, then node `0` is the twin of node `3`, and node `1` is the twin of node `2`. These are the only nodes with twins for `n = 4`.

The **twin sum** is defined as the sum of a node and its twin.

Given the `head` of a linked list with even length, return _the **maximum twin sum** of the linked list_.

## solution

The idea is here is pretty simple. We use a slow and fast pointer strategy to find the middle node of the linked list, and then reverse the second half using two pointers.

Finally, we compute all of the twin sums and take the biggest one.

```python
def pairSum(self, head: Optional[ListNode]) -> int:
	def reverse(node):
		prev, cur = None, node
		while cur:
			temp = cur.next
			cur.next = prev
			prev = cur
			cur = temp
		return prev
  
	# get pointer to n//2-1 index node
	slow = fast = head
	while fast and fast.next and fast.next.next:
		slow = slow.next
		fast = fast.next.next

	# reverse second half
	slow.next = reverse(slow.next)

	# compute all twin sums and take max
	ans = 0
	p1, p2 = head, slow.next
	  
	while p1 and p2:
		ans = max(ans, p1.val + p2.val)
		p1 = p1.next
		p2 = p2.next

	return ans
```
