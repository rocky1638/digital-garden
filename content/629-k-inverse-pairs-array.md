---
type: leetcode
title: 629. k inverse pairs array
tags:
  - dp
  - recursion
  - memoization
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-15
updated: 2024-09-15
---

For an integer array `nums`, an **inverse pair** is a pair of integers `[i, j]` where `0 <= i < j < nums.length` and `nums[i] > nums[j]`.

Given two integers n and k, return the number of different arrays consisting of numbers from `1` to `n` such that there are exactly `k` **inverse pairs**. Since the answer can be huge, return it **modulo** `109 + 7`.

## solutions

Ok, this one’s pretty crazy. The most important intuition is the following:

Given some array, the number of inverse pairs is equal to the number of shift-left transformations are done, when compared to the solely ascending array. (When considering shifted elements in ascending order).

For example, given the array `[4,2,1,3]`, we see from a high level that 2 has been shifted left by one (to the left of 1), and 4 has been shifted three times. So, we have 4 inverse pairs (we can confirm this - `(4,2), (4,1), (4,3), (2,1)`).

### naive dp

With the above intuition, we can start realizing that there is some sort of optimal substructure. Let $dp(n, k)$ represent the number of permutations of $[1,n]$ with $k$ inverse pairs.

Start by considering the base case of $n=1$. We know that there is only one possible permutation, and it has 0 inverse pairs.

Now, consider adding $2$ to this array. We can insert either before or after the $1$. If we insert before $1$, we create an inverse pair. If we insert after $1$, we do not.

This concept can be generalized. Given a subarray permutation of $n$ elements and $k$ inverse pairs, we have $n+1$ options to insert the next value, $n+1$, into the array. If we insert at the leftmost possible position (index 0), our new array permutation has $n+k$ inverse pairs. On the opposite end, if we insert after all existing elements, our new array still has $k$ inverse pairs.

Generalized, if we insert at index $i$, our new $n+1$ array has $n+k-i$ inverse pairs.

With this in mind, we can build up a solution to $dp(n, k)$ by first starting with $dp(1, [0-k])$, and build up each next row for $n+1$ until we reach our final $n$ value.

```python
# O(n*nk) = O(n^2 k)
def kInversePairs(self, n: int, k: int) -> int:
	# base case, n=1 for all values 0-k
	dp = [1]+[0]*k
	prev_n = 1
	  
	for _ in range(n-1):
		new_row = [0]*(k+1)
	  
		for pk, count in enumerate(dp):
			if count > 0:
				for insertion in range(0, prev_n+1):
					if prev_n+pk-insertion <= k:
						new_row[prev_n+pk-insertion] += count
						new_row[prev_n+pk-insertion] %= (10**9+7)
		dp = new_row
		prev_n += 1
	  
	return dp[-1]
```

### optimized dp w/ sliding window

In the above solution, I look through each $k$ value for the previous $n$ value, and then simulate each possible insertion to increment the new $k$ value ($n+k-i$) in the next row.

However, we importantly can realize that the value at $dp(n, k)$ is just the sum of $dp(n-1, k) + dp(n-1, k-1) … dp(n, k-(n-1))$.

To avoid an unnecessary $O(n)$ loop for each $k$ value, we can maintain a sliding window sum from $k$ to $k-n+1$, and setting $dp(n, k)$ to this cumulative sum.

```python
# O(nk)
def kInversePairs(self, n: int, k: int) -> int:
	# base case, n=1 for all values 0-k
	dp = [1]+[0]*k
	prev_n = 1
	  
	for _ in range(n-1):
		new_row = [0]*(k+1)
		window_sum = 0
	  
		for _k in range(k+1):
			window_sum += dp[_k]
			if _k > prev_n:
				window_sum -= dp[_k-prev_n-1]
			new_row[_k] = window_sum % (10**9+7)

		dp = new_row
		prev_n += 1
	
	return dp[-1]
```
