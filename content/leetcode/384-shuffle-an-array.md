---
type: leetcode
title: 384. shuffle an array
tags:
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-08-26
---

Given an integer array `nums`, design an algorithm to randomly shuffle the array. All permutations of the array should be **equally likely** as a result of the shuffling.

Implement the `Solution` class:

- `Solution(int[] nums)` Initializes the object with the integer array `nums`.
- `int[] reset()` Resets the array to its original configuration and returns it.
- `int[] shuffle()` Returns a random shuffling of the array.

## solutions

### sorting

My initial intuition was to assign each number in our array a random number in the range $[0, n-1]$, and then sort based on those numbers.

The runtime here is $O(n \log n)$.

```python
class Solution:
	def __init__(self, nums: List[int]):
		self.original = nums
	
	def reset(self) -> List[int]:
		return self.original
	
	  
	
	def shuffle(self) -> List[int]:
		used = set()
		random_assignments = []
		for num in self.original:
			assignment = random.randrange(0, len(self.original))
			while assignment in used:
				assignment = random.randrange(len(self.original))
		  
		random_assignments.append((num, assignment))
		used.add(assignment)
		  
		random_assignments.sort(key=lambda x: x[1])
		return [x[0] for x in random_assignments]
```

### swapping

Instead of sorting, we can actually do in-place swaps as we go through the array. For each index, we swap it with a random value to the right in the array.

A proof of this method can be found [here](https://people.cs.umass.edu/~phaas/CS590M/handouts/Fisher-Yates-proof.pdf).

> [!note] Some more intuition
> An interesting way to think about this is to imagine how you would go about sorting the list of `[1,2,3]`. We could think about of recursively, first randomly picking an index to place the `1`. Then, in each of the subsequent paths, we pick a random index for `2` out of the remaining indices.
>
> Logically, **it is equivalent to pick a value for the first index, instead of picking an index for the first value!**
>
> This conveniently leads us to the solution below, where we can pick any value from `[0,n-1]` to swap and place at index 0. Then, we can consider the array from `[1,n-1]`, picking a remaining value to be placed at index 1.

```python
class Solution:
	def __init__(self, nums: List[int]):
		self.original = nums
		self.n = len(nums)
	  
	def reset(self) -> List[int]:
		return self.original
	  
	def shuffle(self) -> List[int]:
		copy = self.original[:]
	  
		for i in range(self.n):
			swap_idx = random.randrange(i, self.n)
			copy[i], copy[swap_idx] = copy[swap_idx], copy[i]
		return copy
```
