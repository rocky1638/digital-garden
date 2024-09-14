---
type: leetcode
title: 394. decode string
date: 2022-11-17
updated: 2024-09-01
tag:
---

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed `105`.

## solutions

### recursive

We use recursion to evaluate nested brackets. When we see an opening bracket, we know to go into a recursive call, and to return when we see a closing bracket.

Each recursive call returns the next index that needs to be evaluated *(after its closing bracket)*, and the result of the string decoded within its bounds, very similar to [[224-basic-calculator]].

```python
class Solution:
    def decodeString(self, s: str) -> str:
        def recurse(l):
            acc = ""
            multiplier = None
            
            while l < len(s):
                c = s[l]
                if c.isnumeric():
                    multiplier = c
                    l += 1
                    while l < len(s) and s[l].isnumeric():
                        multiplier += s[l]
                        l += 1
                    multiplier = int(multiplier)
                elif c == "[":
                    next_idx, val = recurse(l+1)
                    acc += multiplier * val
                    l = next_idx
                elif c == "]":
                    return l+1, acc
                else:
                    acc += c
                    l += 1
            return len(s)-1, acc
        
        _, ans = recurse(0)
        return ans
```

### iterative stack

Instead of recursing, we can maintain a stack of multipliers and partial strings. Everytime we reach an opening bracket, we save the multiplier and the current string `piece` for later. When we reach a closing bracket, we know we need to multiply the current string `piece` by our most recent multiplier. The result of this becomes our new `piece`, as we continue iteration now that we’ve exited a bracket pair.

```python
def decodeString(self, s: str) -> str:
	count_stack = []
	string_stack = []
	piece = []
	num = 0
	  
	for c in s:
		if c.isnumeric():
			num *= 10
			num += int(c)
		elif c.isalpha():
			piece.append(c)
		elif c == "[":
			count_stack.append(num)
			num = 0
			string_stack.append(piece)
			piece = []
		elif c == "]":
			piece = string_stack.pop() + (count_stack.pop() * piece)
	return "".join(piece)
```
