---
type: leetcode
title: 8. string to integer
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-03
updated: 2024-08-03
---

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer.

The algorithm for `myAtoi(string s)` is as follows:

1. **Whitespace**: Ignore any leading whitespace (`" "`).
2. **Signedness**: Determine the sign by checking if the next character is `'-'` or `'+'`, assuming positivity is neither present.
3. **Conversion**: Read the integer by skipping leading zeros until a non-digit character is encountered or the end of the string is reached. If no digits were read, then the result is 0.
4. **Rounding**: If the integer is out of the 32-bit signed integer range `[-231, 231 - 1]`, then round the integer to remain in the range. Specifically, integers less than `-231` should be rounded to `-231`, and integers greater than `231 - 1` should be rounded to `231 - 1`.

Return the integer as the final result.

## solution

Basically, just follow the rules. The one tricky part is how to determine the max and min ranges in an environment where numbers can’t go above those values.

We can do some logic based on `INT_MAX/10`. (Logic below from Leetcode editorial).

So there could be 3 cases:

- Case 1: If the current number is less than **INT_MAX / 10 = 214748364**, we can append any digit, and the new number will always be less than **INT_MAX**.

```javascript
'214748363' (less than INT_MAX / 10) + '0' = '2147483630' (less than INT_MAX)
'214748363' (less than INT_MAX / 10) + '9' = '2147483639' (less than INT_MAX)
'1' (less than INT_MAX / 10) + '9' = '19' (less than INT_MAX) 
```

- Case 2: If the current number is more than **INT_MAX / 10 = 214748364**, appending any digit will result in a number greater than **INT_MAX**.

```javascript
'214748365' + '0' = '2147483650' (more than INT_MAX)
'214748365' + '9' = '2147483659' (more than INT_MAX)
'2147483646' + '8' = '21474836468' (more than INT_MAX)
```

- Case 3: If the current number is equal to **INT_MAX / 10 = 214748364**, we can only append digits from **0-7** such that the new number will always be less than or equal to **INT_MAX**.

```python
'214748364' + '0' = '2147483640' (which is less than INT_MAX)
'214748364' + '7' = '2147483647' (which is equal to INT_MAX)
'214748364' + '8' = '2147483648' (which is more than INT_MAX)
```

```python
def myAtoi(self, s: str) -> int:
	# remove whitespace
	s = s.strip()
	if not len(s):
		return 0
	  
	# determine polarity
	polarity = 1
	if s[0] == "+":
		s = s[1:]
	elif s[0] == "-":
		polarity = -1
		s = s[1:]
	  
	s = s.lstrip("0")
	  
	ans = 0
	for digit in s:
		if not digit.isnumeric():
			break
		ans *= 10
		ans += int(digit)
	  
	val = ans*polarity
	if val > 2**31-1:
		return 2**31-1
	elif val < -2**31:
		return -2**31
	return val
```
