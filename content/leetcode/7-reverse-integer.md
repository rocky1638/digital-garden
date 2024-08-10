---
type: leetcode
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/reverse-integer/
title: 7. reverse integer
tags:
  - math
date: 2023-01-01
updated: 2024-08-08
---

Given a signed 32-bit integer `x`, return `x` _with its digits reversed_. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-231, 231 - 1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

## solution

Use some math including modulus and integer division to build up the answer in reverse.

```python
class Solution:
    def reverse(self, x: int) -> int:
        isNegative = False
        if x < 0:
            isNegative = True
            x = abs(x)

        ans = 0
        while x > 0:
            last_digit = x % 10
            ans *= 10
            ans += last_digit

            if ans > 2 ** 31: return 0

            x = x // 10
        return -ans if isNegative else ans
```

The above solution doesn’t account for overflow, so we can instead add some conditions to anticipate overflow and return early, very similar to the logic seen in the solution for [[8-string-to-integer]].

```python
def reverse(self, x: int) -> int:
	INT_MAX = 2**31-1
	INT_MIN = -(2**31)
	  
	is_neg = False
	if x < 0:
		is_neg = True
		x *= -1
	  
	ans = 0
	while x > 0:
		num_to_add = x % 10
	  
		if ans > INT_MAX // 10:
			return 0
		if ans == INT_MAX // 10:
			if is_neg:
				if num_to_add > 8:
					return 0
			else:
				if num_to_add > 7:
					return 0
	  
		ans *= 10
		ans += num_to_add
	  
		# pop off last digit from x
		x //= 10

	return -ans if is_neg else ans
```
