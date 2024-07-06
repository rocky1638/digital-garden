---
type: leetcode
title: 1383. maximum performance of a team
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-12
---

You are given two integers `n` and `k` and two integer arrays `speed` and `efficiency` both of length `n`. There are `n` engineers numbered from `1` to `n`. `speed[i]` and `efficiency[i]` represent the speed and efficiency of the `ith` engineer respectively.

Choose **at most** `k` different engineers out of the `n` engineers to form a team with the maximum **performance**.

The performance of a team is the sum of its engineers' speeds multiplied by the minimum efficiency among its engineers.

Return _the maximum performance of this team_. Since the answer can be a huge number, return it **modulo** `109 + 7`.

## solutions

### sorting by efficiency (asc) + heap

This $O(nk\log n)$ solution times out.

```python
def maxPerformance(self, n: int, speed: List[int], efficiency: List[int], k: int) -> int:
	engs = [(e, s, i) for i, (e, s) in enumerate(zip(efficiency, speed))]
	# efficiency, ascending
	engs.sort(key=lambda x: x[0])
	  
	speed_max_heap = [(-s, e, i) for i, (e, s) in enumerate(zip(efficiency, speed))]
	heapify(speed_max_heap)
	  
	ans = 0
	for eff, sp, idx in engs:
		acc = sp
		ans = max(ans, acc * eff)

		# pop engs that we've moved past
		while speed_max_heap and (
			speed_max_heap[0][1] < eff
			or speed_max_heap[0][2] == idx
		):
			heappop(speed_max_heap)

	popped = []
	# construct all teams from length 2 -> k
	while len(popped) < (k-1) and speed_max_heap:
		neg_s, e, i = heappop(speed_max_heap)
		if i != idx and e >= eff:
			acc -= neg_s
			popped.append((neg_s, e, i))
			ans = max(ans, acc * eff)

	for eng in popped:
		heappush(speed_max_heap, eng)

	return ans % (10**9+7)
```

### sorting by efficiency (desc) + heap

The main efficiency from the solution above is that we have to constantly pop $k$ elements, and re-push $k$ elements to the heap for each engineer that we iterate through. Furthermore, there is repeated work when we potentially keep popping and pushing the same engineers.

The key insight here is that instead of doing this repeated work, we can instead iterate through the engineers in decreasing order of efficiency.

We can then go through each engineer $E$, and compute the best team of engineers where $E$ is the least efficient engineer on the team. However, unlike the above solution, we can maintain a heap of length $k$ that contains the engineers with the highest speed. Furthermore, we know that every speed in this heap belongs to an engineer that is equal or more efficient than the current engineer $E$, so we don't even have to worry about checking efficiencies.

> [!warning]
> If we had tried to do this strategy with the engineers sorted in ascending order, we would have to manually find the minimum efficiency of all the speeds in our heap, which would take an additional worst case $k\log k$ time for each iteration, adding on a $nk\log k$ component to our runtime.

This ultimately achieves a significantly better runtime of $O(n\log k)$.

```python
def maxPerformance(self, n: int, speed: List[int], efficiency: List[int], k: int) -> int:
	engs = sorted(zip(efficiency, speed), reverse=True)
	h = []
	ans = 0
	hsum = 0
	  
	for e, s in engs:
		heappush(h, s)
		hsum += s
		if len(h) > k:
			hsum -= heappop(h)
		ans = max(ans, hsum * e)
	  
	return ans % (10**9+7)
```
