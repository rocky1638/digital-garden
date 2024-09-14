---
type: leetcode
title: 347. top k frequent elements
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/top-k-frequent-elements/
date: 2023-01-03
updated: 2024-08-31
tags:
  - heap
  - bucket-sort
---

## solutions

### heap

- we use a min-heap of length $k$ to store the best most frequent elements that we get from a `Counter` or frequency map.

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        cnt = collections.Counter(nums)
        heap = []

        for val, count in cnt.items():
            if len(heap) < k:
                heapq.heappush(heap, (count, val)) 
            else:
                if count > heap[0][0]:
                    heapq.heappushpop(heap, (count, val))

        return [x[1] for x in heap]
```

### bucket sort

Since the number of frequencies is bounded by the length of `nums`, we can bucket sort our values and then just flatten/take the top `k`.

```python
def topKFrequent(self, nums, k):
	bucket = [[] for _ in range(len(nums) + 1)]
	c = Counter(nums)
	for num, freq in c.items():
		bucket[freq].append(num)
	flat_list = [item for sublist in bucket for item in sublist]
	return flat_list[::-1][:k]
```
