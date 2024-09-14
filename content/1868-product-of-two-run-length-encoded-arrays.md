---
type: leetcode
title: 1868. product of two run-length encoded arrays
tags:
  - two-pointer
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-01
updated: 2024-09-01
---

**Run-length encoding** is a compression algorithm that allows for an integer array `nums` with many segments of **consecutive repeated** numbers to be represented by a (generally smaller) 2D array `encoded`. Each `encoded[i] = [vali, freqi]` describes the `ith` segment of repeated numbers in `nums` where `vali` is the value that is repeated `freqi` times.

- For example, `nums = [1,1,1,2,2,2,2,2]` is represented by the **run-length encoded** array `encoded = [[1,3],[2,5]]`. Another way to read this is "three `1`'s followed by five `2`'s".

The **product** of two run-length encoded arrays `encoded1` and `encoded2` can be calculated using the following steps:

1. **Expand** both `encoded1` and `encoded2` into the full arrays `nums1` and `nums2` respectively.
2. Create a new array `prodNums` of length `nums1.length` and set `prodNums[i] = nums1[i] * nums2[i]`.
3. **Compress** `prodNums` into a run-length encoded array and return it.

You are given two **run-length encoded** arrays `encoded1` and `encoded2` representing full arrays `nums1` and `nums2` respectively. Both `nums1` and `nums2` have the **same length**. Each `encoded1[i] = [vali, freqi]` describes the `ith` segment of `nums1`, and each `encoded2[j] = [valj, freqj]` describes the `jth` segment of `nums2`.

Return _the **product** of_ `encoded1` _and_ `encoded2`.

**Note:** Compression should be done such that the run-length encoded array has the **minimum** possible length.

## solutions

The problem is a pretty standard two-pointer approach, just don’t expand, but instead, take the product of as many matching values of the short RLE section, and modify the RLE in place.

```python
def findRLEArray(self, encoded1: List[List[int]], encoded2: List[List[int]]) -> List[List[int]]:
	res = []
	p1 = p2 = 0
	  
	def add(val, length):
		if not res or res[-1][0] != val:
			res.append([val, length])
		else:
			res[-1][1] += length

	while p1 < len(encoded1) and p2 < len(encoded2):
		v1, l1 = encoded1[p1]
		v2, l2 = encoded2[p2]
		if l1 == l2:
			add(v1*v2, l1)
			p1 += 1
			p2 += 1
		elif l1 < l2:
			add(v1*v2, l1)
			encoded2[p2][1] -= l1
			p1 += 1
		else:
			add(v1*v2, l2)
			encoded1[p1][1] -= l2
			p2 += 1
	return res
```
