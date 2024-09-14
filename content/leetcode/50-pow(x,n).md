---
type: leetcode
title: 50. pow(x, n)
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/powx-n/
date: 2022-12-29
updated: 2024-08-28
---

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., `xn`).

## solutions

### recursion w/ memoization

- i first tried to do it linearly by just multiplying $x$ repeatedly by itself, but that was too slow.
- then, i realized that you can [[divide-and-conquer]] by splitting the exponent in half each time and using [[recursion]].
- this still timed out, so i realized that there were many computations that were being repeated, so decided to use [[memoization]] to speed up the process significantly.

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0: return 1
        if n < 0:
            n = abs(n)
            x = 1/x

        memo = {}
        def recurse(val, exp):
            if exp == 1:
                return val
            
            first_half = exp // 2
            second_half = exp - first_half

            if first_half in memo: val1 = memo[first_half] 
            else:
                val1 = recurse(val, first_half)
                memo[first_half] = val1

            if second_half in memo: val2 = memo[second_half] 
            else:
                val2 = recurse(val, second_half)
                memo[second_half] = val2

            return val1 * val2

        return recurse(x, n)
```

### iterative

Instead of splitting the exponent in half, we can just set `x *= x` whenever we have an even exponent, halving the exponent and reducing our calculations by 50%.

```python
def myPow(self, x: float, n: int) -> float:
	if n == 0:
		return 1
	  
	if n < 0:
		x = 1./x
		n *= -1
		
	ans = 1
	while n != 0:
		if n % 2 == 1:
			ans *= x
			n -= 1
		else:
			x *= x
			n //= 2
	return ans
```
