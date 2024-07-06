---
type: leetcode
title: 837. new 21 game
tags:
  - dp
  - math
aliases: 
parents: 
children: 
supports:
  - "[[70-climbing-stairs]]"
enemies: 
date: 2022-12-30
updated: 2024-06-30
---

Alice plays the following game, loosely based on the card game **"21"**.

Alice starts with `0` points and draws numbers while she has less than `k` points. During each draw, she gains an integer number of points randomly from the range `[1, maxPts]`, where `maxPts` is an integer. Each draw is independent and the outcomes have equal probabilities.

Alice stops drawing numbers when she gets `k` **or more points**.

Return the probability that Alice has `n` or fewer points.

Answers within $10^{-5}$ of the actual answer are considered accepted.

## solution

First of all, we have to figure out the math here. The probability we’re looking for is the probability that we end up in any of the point scores in the range $[K, N]$ (because we only stop once our score is at least $K$).

Immediately, it’s clear that we *could* enumerate all of the possible jumps, but that would be polynomial in complexity and time out. However, it’s pretty intuitive to see that some sort of subproblem structure exists here and that dynamic programming is possible.

---

Let $W$ be equal to `maxPts`.

The first insight is that from any point score $P$, we have a uniform $1/W$ probability of reaching all of the next points in the range $[P+1, P+W]$.

The key insight then to make the dynamic programming easy is to reverse the logic and look backwards. Imagine that $W=3$, and we have some point $P_4$. We see that from each of $P_1, P_2$, and $P_3$, we have a probability of $1/W$ or $\frac13$ to reach $P_4$.

Thus, $P(P_4) = \frac1W P_1 + \frac1W P_2 + \frac1W P_3$ which ultimately simplifies to $\frac1W(P_1+P_2+P_3)$.

So, translating this into code, we realize that `dp[i]` is equal to `1/maxPts * sum(dp[i-maxPts:i]`. If we keep a sliding window sum, we can do these calculations in constant time!

Finally, our answer is the sum of all the probabilities of reaching the range $[K,N]$.

```python
def new21Game(self, n: int, k: int, maxPts: int) -> float:
	if k == 0 or n >= k + maxPts:
		return 1.0
	  
	dp = [1.0] + [0.0]*n
	  
	window_sum = 1.0
	for i in range(1, n+1):
		dp[i] = window_sum / maxPts
		if i < k: window_sum += dp[i]
		if i - maxPts >= 0: window_sum -= dp[i-maxPts]
	return sum(dp[k:])
```
