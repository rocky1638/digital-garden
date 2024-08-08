---
type: leetcode
title: 564. find the closest palindrome
tags:
  - math
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-02-24
---

Given a string `n` representing an integer, return _the closest integer (not including itself), which is a palindrome_. If there is a tie, return _**the smaller one**_.

The closest is defined as the absolute difference minimized between two integers.

## solution

The key intuition is that, (ignoring edge cases), we want to change the values at the _middle_ of the number to reach the next palindrome with the smallest change in value. This is because if we change values more towards the edges of the number, the value on the left will be a more significant bit, and cause more change in the value of the end number.

In considering changing the central values, we know that we’ll only want to change the values by plus or minus one. We have to deal with many different cases, including:

- Even length number.
- Odd length number.
- Number that’s already a palindrome.
- Numbers near the boundary of a length, e.g. 999, 1000.
- 1001 as well, the closest is 999.

Now to implement this in code, we first get the prefix of the number, and consider palindromes that use that prefix, or the prefix above/below it.

For example, for 12345, the prefix will be 123 (likewise, for 1234, the prefix is 12). The palindrome for this prefix would be 12321 or 1221, respectively. We can then also consider the prefixes 122/124 or 11/13 (with palindromes 12221/12421 and 1111/1331). We then just return the value with the smallest diff.

```python

```
