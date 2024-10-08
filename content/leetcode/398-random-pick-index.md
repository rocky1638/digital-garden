---
type: leetcode
title: 398. random pick index
tags:
  - reservoir-sampling
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-30
updated: 2024-08-30
---

Given an integer array `nums` with possible **duplicates**, randomly output the index of a given `target` number. You can assume that the given target number must exist in the array.

Implement the `Solution` class:

- `Solution(int[] nums)` Initializes the object with the array `nums`.
- `int pick(int target)` Picks a random index `i` from `nums` where `nums[i] == target`. If there are multiple valid i's, then each index should have an equal probability of returning.

## solutions

### reservoir sampling

This is a really elegant and clean technique to picking from $n$ elements in a stream with equal probability.

Essentially at each step in the stream that we see the $k$th element, we have a $1/k$ probability of selecting it. Over $n$ elements, we can be guaranteed to ultimately pick each element with probability $1/n$.

Here’s a proof:

**Base case**: The algorithm trivially works for $n=1$.

**Induction assumption**: For a stream with $n$ elements, all elements are chosen with the same final probability $1/n$.

**Inductive step**: Consider the case where $n=n+1$. We want to show that for a stream of $n+1$ elements, all items still have the same probability of $1/(n+1)$ to be sampled.

The algorithm tells us to choose the next element of the stream with a probability of $1/(n+1)$. All other elements can be the current reservoir element with a probability of $1/n$ by the induction assumption.

The current reservoir element has a probability of $1−1/(n+1)=n/(n+1)$ to stay. This means all previous elements have a final probability of $(n/(n+1))\cdot(1/n)=1/(n+1)$ to be the reservoir element after this step. Thus, all elements still have the same probability of being selected as the reservoir element.

```python
class Solution:
	def __init__(self, nums: List[int]):
		self.nums = nums
	  
	def pick(self, target: int) -> int:
		count = 0
		ans = None
	  
		for i, num in enumerate(self.nums):
			if num == target:
				count += 1
				choice = randint(1, count)
				if choice == count:
					ans = i
	return ans
```

### hashmap + random int

We can first store the indices for each value, and then just pick a random one.

```python
class Solution:
	def __init__(self, nums: List[int]):
		self.freq = defaultdict(list)
		for i, num in enumerate(nums):
			self.freq[num].append(i)
	  
	def pick(self, target: int) -> int:
		choice = random.randint(0, len(self.freq[target])-1)
		return self.freq[target][choice]
```
