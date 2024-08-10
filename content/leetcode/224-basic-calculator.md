---
type: leetcode
title: 224. basic calculator
date: 2022-11-25
updated: 2024-08-09
tags:
  - recursion
  - string
  - math
---

Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return _the result of the evaluation_.

**Note:** You are **not** allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

## solution

Intuitively, we know we need recursion for brackets, but the hard part is figuring out how to orchestrate everything.

My strategy for this is to keep two running variables, a `tally`, which keeps track of the evaluated value so far, and `prev_op`, which tracks the operation we will perform on `tally` once we see our next number.

Naturally, `prev_op` begins as addition, as when we see our first number, we’ll add it to our initial `tally` of 0.

Then, to handle recursion, we enter recursion when we see an opening bracket and return when we see a closing bracket. Note that the end of the recursion should tell us what value was accumulated within the brackets, as well as where we should pick up our looping again.

```python
class Solution:
    def calculate(self, s: str) -> int:
        # helper function        
        def evalExpression(op, x, y):
            if op == "+":
                return x + y
            elif op == "-":
                return x - y
        
        def recurse(idx):
            tally = 0
            prev_op = "+"
            
            while idx < len(s):
                char = s[idx]
                
                if char == "(":
                    idx, subtally = recurse(idx+1)
                    tally = evalExpression(prev_op, tally, subtally)
            
                elif char == ")":
                    return idx+1, tally
                
                elif char.isnumeric():
                    num_str = char
                    idx += 1
                    while idx < len(s) and s[idx].isnumeric():
                        num_str += s[idx]
                        idx += 1
                    tally = evalExpression(prev_op, tally, int(num_str))
                elif char in ["+", "-"]:
                    prev_op = char
                    idx += 1
                else:
                    idx += 1
            return tally
                
        return recurse(0)
```
