---
type: leetcode
title: 73. set matrix zeroes
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/set-matrix-zeroes/
date: 2023-01-01
updated: 2024-09-11
---

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

## solution

We use a sentinel value to mark values as being cleared in place.

We also use sets to keep track of rows/columns that we’ve already cleared so we don’t repeat operations.

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        seenRows = set()
        seenCols = set()

        def zeroCross(x, y):
            # clear row
            if x not in seenRows:
                for i in range(len(matrix[x])):
                    if matrix[x][i] != 0:
                        matrix[x][i] = None
                seenRows.add(x)
            
            # clear col
            if y not in seenCols:
                for j in range(len(matrix)):
                    if matrix[j][y] != 0:
                        matrix[j][y] = None
                seenCols.add(y)


        for i in range(len(matrix)):
            for j in range(len(matrix[i])):
                if matrix[i][j] == 0:
                    matrix[i][j] = None
                    zeroCross(i, j)

        for i in range(len(matrix)):
            for j in range(len(matrix[i])):
                if matrix[i][j] is None:
                    matrix[i][j] = 0
```

As a minor optimization, instead of zeroing out the entire cross with a sentinel value, we can just mark a row/col to be zeroed by setting the first value in the row/col as zero. We are safe to do this because if we iterate normally, we will have already seen the first value in the row/col for any time we see a zero (so we won’t accidentally zero more things than we should).
