---
type: leetcode
title: 344. increasing triplet subsequence
tags:
  - two-pointer
aliases: 
parents:
  - "[[300-longest-increasing-subsequence]]"
children: 
supports: 
enemies: 
date: 2024-09-27
updated: 2024-09-27
---

Given an integer array `nums`, return `true` _if there exists a triple of indices_ `(i, j, k)` _such that_ `i < j < k` _and_ `nums[i] < nums[j] < nums[k]`. If no such indices exists, return `false`.

## solutions

### two pointers

The main intuition here is that if we iterate through the array, when we see a smaller number, we can choose to “restart” our triplet building or not. However, what happens when we see a value that’s smaller than our first value, when we’ve already constructed a pair of numbers?

If there’s only one more really big number after this number and we reset, we lose out on the valid answer. Call our smallest number index `i` and our middle number index `j`.

The weirdness here is that when we update `i`, we don’t actually need to update `j`. This is because even if `i` is updated to be $>j$, we don’t care because if we find a valid third value, we know that there USED to be a value `i` that was smaller and left of `j`, so there is a valid triplet.

Consider the test case `[1,2,0,3]` to visualize this!

---

We use two pointers to keep track of our smallest and second smallest values seen so far.

If we ever see a value smaller than `i`, we update `i`. Falling through, if the value is smaller than `j`, we update `j`.

If those cases don’t hold, if we ever see a value larger than `j`, we can return `true`.

```java
class Solution {
	public boolean increasingTriplet(int[] nums) {
		int i = -1;
		int j = -1;
		  
		for (int x=0; x < nums.length; x++) {
			if (i < 0 || nums[x] <= nums[i]) {
				i = x;
			} else if (j < 0 || nums[x] <= nums[j]) {
				j = x;
			} else if (i >= 0 && j >= 0 && nums[x] > nums[j]) {
				return true;
			}
		}
		return false;
	}
}
```
