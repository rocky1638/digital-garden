---
type: leetcode
title: 1545. find kth bit in nth binary string
tags:
  - divide-and-conquer
  - recursion
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-22
updated: 2024-10-22
---

Given two positive integers `n` and `k`, the binary string `Sn` is formed as follows:

- `S1 = "0"`
- `Si = Si - 1 + "1" + reverse(invert(Si - 1))` for `i > 1`

Where `+` denotes the concatenation operation, `reverse(x)` returns the reversed string `x`, and `invert(x)` inverts all the bits in `x` (`0` changes to `1` and `1` changes to `0`).

For example, the first four strings in the above sequence are:

- `S1 = "0"`
- `S2 = "0**1**1"`
- `S3 = "011**1**001"`
- `S4 = "0111001**1**0110001"`

Return _the_ `kth` _bit_ _in_ `Sn`. It is guaranteed that `k` is valid for the given `n`.

## solutions

### simulation

We can simulate constructing the strings, where the last string will be of length $2^n$.

```python
# O(2^n)
def findKthBit(self, n: int, k: int) -> str:
	flip = {"0": "1", "1": "0"}

	def invert(s):
		return [flip[c] for c in s]

	def recurse(i):
		if i == 1:
			return ["0"]
		prev = recurse(i-1)
		return prev + ["1"] + invert(prev[::-1])

	s = recurse(n)
	return s[k-1]
```

### divide and conquer

We can divide and conquer, updating $k$ as necessary.

An explanation for the case when $k$ is in the second half is as follows.

If for some $S_n$, we have $k > m$, we know that we’re looking for the $k-m$ positioned value in a _reversed_ $S_{n-1}$. This means that when we would normally index by $k-m$, we instead need to index by the reflection over $m$.

As a concrete example, imagine we have length of $S_n = 7$, and $k = 5$.

```
S_3 = 0111001
		    ^
		    k
k = 5
```

Note that the “001” is actually a reversed/inverted version of $S_2$. As such, when we recursively compute $S_2$, we actually want to select for the _third_ value of $S_2$, and not the first value (which is what it appears like we’re doing with the current value of $k$).

```
S_3 = 0111001
		    ^
		    k
S_3 = S_2 + "1" + reverse(invert(S2))
=> S_3 = 011 1 reverse(invert(011))
										  ^
										  k
=> S_3 = 011 1 invert(110)
						    ^
						    k
k = 5
```

So, to invert over the $m$ value, we do $l-k$, and then add 1 to account for the middle element.

```python
# O(n)
def findKthBit(self, n: int, k: int) -> str:
	def recurse(_n, _k):
		# Base case for the smallest sequence, S1 = "0"
		if _n == 1:
			return "0"
		  
		# Length of the sequence for S_n is 2^n - 1
		l = (1 << _n) - 1
		# Midpoint of the sequence
		m = (l + 1) // 2
		  
		# If k is at the midpoint, the result is always "1"
		if _k == m:
			return "1"
		# If k is in the first half, recurse directly
		if _k < m:
			return recurse(_n - 1, _k)
		# If k is in the second half, reflect and invert
		if _k > m:
			# if we're looking for kth element in s_n of length l,
			# it's in the second half, so when we index s_(n-1),
			# we actually
			# reflected k = -(_k-l) = l-_k
			# +1 to handle one-indexing
			reflected_k = l - _k + 1 # Reflect k over the midpoint
			ans = recurse(_n - 1, reflected_k)
			return "0" if ans == "1" else "1" # Invert the result
	
	return recurse(n, k)
```
