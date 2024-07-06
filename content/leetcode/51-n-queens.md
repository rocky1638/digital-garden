---
created_at: 2023-01-11
type: leetcode
aliases: 
difficulty: 🔴
link: https://leetcode.com/problems/n-queens/
tags:
  - backtracking
date: 2023-01-11
updated: 2024-05-28
---

# 51. N Queens

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

## solution

At it’s core, this question is pretty simple as we use backtracking to place queens in valid spots.

However, there is a fancy way to store controlled squares by indexing columns, diagonals, and anti-diagonals.

Another small trick is that we ensure the rows don’t overlap by always placing in the next row.

![](https://leetcode.com/problems/n-queens/solutions/1198087/Figures/51/diagonals.png)
![](https://leetcode.com/problems/n-queens/solutions/1198087/Figures/51/antidiagonals.png)

```python
class Solution:
    def solveNQueens(self, n):
        # Making use of a helper function to get the
        # solutions in the correct output format
        def create_board(state):
            board = []
            for row in state:
                board.append("".join(row))
            return board
        
        def backtrack(row, diagonals, anti_diagonals, cols, state):
            # Base case - N queens have been placed
            if row == n:
                ans.append(create_board(state))
                return

            for col in range(n):
                curr_diagonal = row - col
                curr_anti_diagonal = row + col
                # If the queen is not placeable
                if (col in cols 
                      or curr_diagonal in diagonals 
                      or curr_anti_diagonal in anti_diagonals):
                    continue

                # "Add" the queen to the board
                cols.add(col)
                diagonals.add(curr_diagonal)
                anti_diagonals.add(curr_anti_diagonal)
                state[row][col] = "Q"

                # Move on to the next row with the updated board state
                backtrack(row + 1, diagonals, anti_diagonals, cols, state)

                # "Remove" the queen from the board since we have already
                # explored all valid paths using the above function call
                cols.remove(col)
                diagonals.remove(curr_diagonal)
                anti_diagonals.remove(curr_anti_diagonal)
                state[row][col] = "."

        ans = []
        empty_board = [["."] * n for _ in range(n)]
        backtrack(0, set(), set(), set(), empty_board)
        return ans
```
