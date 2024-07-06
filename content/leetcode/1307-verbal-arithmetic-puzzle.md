---
type: leetcode
title: 1307. verbal arithmetic puzzle
tags:
aliases: 
parents: 
children: 
supports: 
enemies:
date: 2022-12-30
updated: 2024-05-25
---

Given an equation, represented by `words` on the left side and the `result` on the right side.

You need to check if the equation is solvable under the following rules:

- Each character is decoded as one digit (0 - 9).
- No two characters can map to the same digit.
- Each `words[i]` and `result` are decoded as one number **without** leading zeros.
- Sum of numbers on the left side (`words`) will equal to the number on the right side (`result`).

Return `true` _if the equation is solvable, otherwise return_ `false`.

## references

- https://leetcode.com/problems/verbal-arithmetic-puzzle/solutions/463921/python-backtracking-with-pruning-tricks
