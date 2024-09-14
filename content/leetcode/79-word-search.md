---
type: leetcode
title: 79. word search
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/word-search/
date: 2022-11-22
updated: 2024-09-02
---

Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

## solution

- this is a pretty classic [[dfs]] problem.
- we go through each character in the grid, and when we see a valid starting character, [[dfs]] through the entire grid to try to complete the target `word`.
- keep a visited set that we `add` and `remove` from _(when we backtrack)_ between `dfs` calls.

```python
def exist(self, board: List[List[str]], word: str) -> bool:
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	visited = set()

	def dfs(i, j, word_idx):
		if word_idx == len(word)-1:
			return True

		res = False
		for d in dirs:
			ni, nj = i + d[0], j + d[1]
			if ni >= 0 and ni < len(board) and nj >= 0 and nj < len(board[0]):
					if (ni,nj) not in visited and board[ni][nj] == word[word_idx+1]:
						visited.add((ni,nj))
						res = res or dfs(ni, nj, word_idx+1)
						visited.remove((ni,nj))
		return res

	for i in range(len(board)):
		for j in range(len(board[0])):
			if board[i][j] == word[0]:
				visited.add((i,j))
				found = dfs(i, j, 0)
				if found:
					return True
				visited.remove((i,j))
	return False
```
