---
title: 658. find k closest elements
type: leetcode
date: 2024-07-19
updated: 2024-09-01
tags:
  - heap
  - binary-search
---

Given a **sorted** integer array `arr`, two integers `k` and `x`, return the `k` closest integers to `x` in the array. The result should also be sorted in ascending order.

An integer `a` is closer to `x` than an integer `b` if:

- `|a - x| < |b - x|`, or
- `|a - x| == |b - x|` and `a < b`

## solutions

### binary search w/ heap

We use binary search to find the center of the window that we search linearly with our heap. We know that the $k$ closest values definitely lie within the range of $[x-k, x+k]$ in our sorted array.

```python
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        """
        1. use binary search to find the closest element to x.
        2. do a linear scan in the window from k elements below x to k elements above x. (maybe k+1 to be safe).
        3. use a max heap to keep track of the k closest numbers we've seen.
        """

        center_idx = bisect.bisect_left(arr, x)
        lb, rb = max(0, center_idx-k-1), min(center_idx+k+1, len(arr)-1)

        heap = []
        for i in range(lb, rb+1):
            if len(heap) < k:
                heapq.heappush(heap, (-abs(x-arr[i]), arr[i]))
            else:
                diff = abs(x-arr[i])
                if (-diff > heap[0][0]) or (-diff == heap[0][0] and arr[i] < heap[0][1]):
                    heapq.heappushpop(heap, (-diff, arr[i]))
        return sorted([x[1] for x in heap])
```

### binary search w/ two pointers

Instead of maintaining a heap, we can take advantage of the knowledge that `arr` is already sorted, and thus the `k` closest elements will be consecutive within the array. Because of this, we can use two pointers, moving whichever pointer yields the closer value, until we have `k` values.

```python
def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
	if len(arr) == k:
		return arr

	# bisect_left lands on the index of the first
	# element that is >= x
	# so, we should look on both "sides" of x, hence
	# we subtract 1 from l, and keep r = bisect_left because
	# arr[r] could == x
	l = bisect_left(arr, x) - 1
	r = l + 1
	  
	# create window (l, r]
	while r-l-1 < k:
		if l == -1:
			r += 1
		elif r == len(arr):
			l -= 1
		else:
			# if left is better, use it
			if abs(arr[l]-x) <= abs(arr[r]-x):
				l -= 1
			else:
				r += 1
	  
	return arr[l+1:r]
```
