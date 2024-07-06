---
type: leetcode
title: 975. odd even jump
tags:
  - monotonic-stack
  - dp
  - sorting
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-21
---

You are given an integer array `arr`. From some starting index, you can make a series of jumps. The (1st, 3rd, 5th, ...) jumps in the series are called **odd-numbered jumps**, and the (2nd, 4th, 6th, ...) jumps in the series are called **even-numbered jumps**. Note that the **jumps** are numbered, not the indices.

You may jump forward from index `i` to index `j` (with `i < j`) in the following way:

- During **odd-numbered jumps** (i.e., jumps 1, 3, 5, ...), you jump to the index `j` such that `arr[i] <= arr[j]` and `arr[j]` is the smallest possible value. If there are multiple such indices `j`, you can only jump to the **smallest** such index `j`.
- During **even-numbered jumps** (i.e., jumps 2, 4, 6, ...), you jump to the index `j` such that `arr[i] >= arr[j]` and `arr[j]` is the largest possible value. If there are multiple such indices `j`, you can only jump to the **smallest** such index `j`.
- It may be the case that for some index `i`, there are no legal jumps.

A starting index is **good** if, starting from that index, you can reach the end of the array (index `arr.length - 1`) by jumping some number of times (possibly 0 or more than once).

Return _the number of **good** starting indices_.

## solutions

### brute force

The brute force solution is trivial to come up with, and involves simulating the jumping process from each index $i$. For each jump, we use a linear scan to find the jump location. All in all, this is $O(n^3)$.

I found that there were two primary places with opportunity to optimize.

1. Repeated work when simulating jump sequences. Just like [[70-climbing-stairs]], we can cache smaller subproblems using dynamic programming.
2. Inefficient calculation of next jump index. If we can calculate this in less than $O(n^2)$ time, we could have a large improvement in performance.

### sortedlist + dp

To solve the first optimization, we use two DP arrays, representing whether we can reach the end from any index $i$ starting with an odd jump or an even jump. I named these arrays `dp_odd` and `dp_even` respectively.

Then, we iterate backwards through `arr`. This cuts out a factor of $O(n)$ from our solution, leaving our current solution at $O(n^2)$.

Next, we need to figure out a way to speed up computation for our next jump index. Initially, I tried thinking of a solution with a balanced tree (or `SortedList`) type structure, that supports lookup, deletion, and insertion in $O(\log n)$ time.

This solution unfortunately timed out, as the worst case performance of `find_odd_index` and `find_even_index` was still $O(n)$.

```python
from sortedcontainers import SortedList

def oddEvenJumps(self, arr: List[int]) -> int:
 n = len(arr)
 arr_asc = SortedList([(arr[-1], n-1)])
 arr_desc = SortedList([(arr[-1], n-1)], key=lambda x: (-x[0], x[1]))

 def find_odd_index(i):
	nonlocal arr
	nonlocal arr_asc
	ret = None
	for num, idx in arr_asc:
	  if num >= arr[i]:
		 ret = idx
		 break

	arr_asc.add((arr[i], i))
	return ret
	
 def find_even_index(i):
	nonlocal arr
	nonlocal arr_desc
	ret = None
	for num, idx in arr_desc:
	  if num <= arr[i]:
		 ret = idx
		 break

	arr_desc.add((arr[i], i))
	return ret

 dp_odd = [False] * n
 dp_even = [False] * n

 # base case 
 dp_odd[-1] = True
 dp_even[-1] = True

 ans = 1

 for i in reversed(range(n-1)):
	next_odd_jump = find_odd_index(i)
	next_even_jump = find_even_index(i)
	
	if next_odd_jump:
	  if dp_even[next_odd_jump]:
		 ans += 1
	  dp_odd[i] = dp_even[next_odd_jump]

	if next_even_jump:
	  dp_even[i] = dp_odd[next_even_jump]

 return ans
```

### sorting + monotonic stack + dp

Finally, although I had a hunch that monotonic stack was possible, I couldn’t quite wrap my head around how to do it.

I’ll explain how the monotonic stack approach works for the next odd jump (finding the next largest element in the array to the right, using closer index as a tiebreaker). The even jump is the exact same logic in reverse.

In the end, I looked at the solution, but the idea here is to first sort the array, and then _maintain a monotonic stack with an increasing index as the invariant_. (Logically, this kind of maintains two invariants).

1. By first sorting the array, we can guarantee that as we loop through and push values onto our stack, each value is $\ge$ than the previous value, which satisfies half of our odd-jump condition.
2. By maintaining a montonically increasing index stack, we know that when we reach a value with value $x$ and index $i$, every value in our stack with index $\lt i$ will also have a value $\le x$. Furthermore, we know it’s the _next_ biggest value that occurs to the right, because every value proceeding will be larger or equal, as our array is sorted.

After solving this “closest next incrementally greater value to right” subproblem, the rest of the solution is the same with dynamic programming.

```python
def oddEvenJumps(self, arr: List[int]) -> int:
	n = len(arr)
	  
	odd_jumps = [-1] * n
	even_jumps = [-1] * n
	  
	stack = []
	for val, i in sorted([val, i] for i, val in enumerate(arr)):
		while stack and stack[-1][1] < i:
			popped, popped_idx = stack.pop()
			odd_jumps[popped_idx] = i
		stack.append((val, i))
	  
	stack = []
	for val, i in sorted([-val, i] for i, val in enumerate(arr)):
		while stack and stack[-1][1] < i:
			popped, popped_idx = stack.pop()
			even_jumps[popped_idx] = i
		stack.append((val, i))
	  
	dp_odd = [False] * n
	dp_even = [False] * n
	  
	# base case
	dp_odd[-1] = True
	dp_even[-1] = True
	  
	ans = 1
	  
	for i in reversed(range(n-1)):
		next_odd_jump = odd_jumps[i]
		next_even_jump = even_jumps[i]

		if next_odd_jump >= 0:
			if dp_even[next_odd_jump]:
			ans += 1
			dp_odd[i] = dp_even[next_odd_jump]
	  
		if next_even_jump >= 0:
			dp_even[i] = dp_odd[next_even_jump]
	  
	return ans
```
