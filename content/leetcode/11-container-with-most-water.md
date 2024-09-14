---
type: leetcode
title: 11. container with most water
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/container-with-most-water/
date: 2022-11-22
updated: 2024-09-10
---

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return _the maximum amount of water a container can store_.

**Notice** that you may not slant the container.

## solution

- we use [[two-pointers]] to move gradually inward from the outside, keeping track of most water stored in `ans`.
- we always move inward with the shorter of the two walls!
	- we can prove this [[greedy]] approach by thinking about the contrary.
	- if we moved in with the taller wall, we would always guarantee that our stored water would be less, because the horizontal distance is decreasing, and even if we found a taller wall, we would still be equally limited by the shorter wall _(that we did not move inwards from)._
	- therefore, we must always move the shorter wall to have a chance at increasing `ans`.

> [!abstract]+ A good proof
> This is a formal proof, beyond the simple greedy idea that “because a wall is no longer going to contribute, we can move past it.” That idea doesn’t adequately prove that we’re guaranteed to reach the global optima.
>
> ---
> The correct solution $A*$ has a left bound of $i*$ and a right bound of $j*$ with a height $h*=\min(h[i*], h[j*])$. At some point of this algorithm's execution, the left pointer i or the right pointer $j$ will point to one of $[i*, j*]$ for the first time. Consider the case where $i=i*$ and $j>j*$
>
> Case 1: $h[j] >= h*$. The container $(i*, j)$ is wider than $(i*, j*)$. If $(i*, j)$ was as tall as $h*$, then it would be bigger than $A*$. This is a contradiction, so this case is impossible.
>
> Case 2: $h[j] < h*$. Because $h* <= h[i]$, this implies that $h[j*] < h[i]$, so we will decrement $j$. This brings us closer to the correct solution, $A*$.
>
> We can repeatedly apply this same logic to every step to decrement j until we reach $j=j*$. At that point, the optimal solution will be recorded.
>
> By symmetry, we are assured that when $j=j*$, then the same logic will allow us to increment $i$ to $i*$.

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        ans = 0
        
        l, r = 0, len(height)-1
        
        while l < r:
            minheight = min(height[l], height[r])
            ans = max(ans, minheight * (r-l))
            
            # how do we move in? greedily keep the larger one
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return ans
```
