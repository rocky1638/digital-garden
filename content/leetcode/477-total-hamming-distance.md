---
type: leetcode
title: 477. total hamming distance
tags:
  - math
  - bit-manipulation
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-27
updated: 2024-09-27
---

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.

Given an integer array `nums`, return _the sum of **Hamming distances** between all the pairs of the integers in_ `nums`.

## solution

The simple solution is to calculate the hamming distance for each pair. This is $O(n^2)$.

### combinatorics by bit

Instead, we can find how many 0s and 1s occur at each bit index. For each 0, we add one hamming distance to each 1. This can be calculated by `numOnes * numZeroes`.

```java
class Solution {
	public int totalHammingDistance(int[] nums) {
		int res = 0;
		  
		for (int i=0; i < 32; i++) {
			int ones = 0;
		  
			for (int j=0; j<nums.length; j++) {
				ones += (nums[j] >> i) & 1;
			}
			res += ones * (nums.length-ones);
		}
		  
		return res;
	}
}
```
