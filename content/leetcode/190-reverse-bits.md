---
type: leetcode
title: 190. reverse bits
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-05-28
---

Reverse bits of a given 32 bits unsigned integer.

**Note:**

- Note that in some languages, such as Java, there is no unsigned integer type. In this case, both input and output will be given as a signed integer type. They should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
- In Java, the compiler represents the signed integers using [2's complement notation](https://en.wikipedia.org/wiki/Two%27s_complement). Therefore, in **Example 2** above, the input represents the signed integer `-3` and the output represents the signed integer `-1073741825`.

## solution

We create an accumulator `res` and initialize it to 0, and then slowly build it up by adding the LSB of `n`, then left-shifting `res`. Then, we right-shift `n` to delete the current LSB and move the next one to the left over into the LSB position.

This way, the bits get reversed and we can return `res`.

```python
def reverseBits(self, n: int) -> int:
	res = 0
	for _ in range(32):
		res <<= 1
		res += n & 1
	  
		n >>= 1
	return res
```
