---
title: 212. word search ii
type: leetcode
aliases: 
difficulty: 🔴
link: https://leetcode.com/problems/word-search-ii/
date: 2023-01-10
updated: 2024-03-26
tags:
  - trie
  - backtracking
---

Given an `m x n` `board` of characters and a list of strings `words`, return _all words on the board_.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

## solution

We create a trie to store the list of words that we’re trying to search for. Then, for each cell in the matrix, if it is the start of a word, we bfs starting from it to try to find a matching word.

```python
class TrieNode:
	def __init__(self, val, isEnd = False):
		self.val = val
		self.children = {}
		self.isEnd = isEnd

class Trie:
	def __init__(self):
		self.root = TrieNode(None)

	def insert(self, word):
		cur = self.root

		for char in word:
			if char in cur.children:
				cur = cur.children[char]
			else:
				new = TrieNode(char)
				cur.children[char] = new
				cur = new
		  
		# cur is on the last character of the word
		cur.isEnd = True
```

```python
def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
	trie = Trie()
	# construct trie from dictionary
	for word in words:
		trie.insert(word)
	  
	ans = []
	dirs = [[0,1],[1,0],[0,-1],[-1,0]]
	visited = set()
	  
	def dfs(x, y, trieNode, acc):
		if trieNode.isEnd:
			ans.append(acc)
			trieNode.isEnd = False # avoid dupes
		  
		for d in dirs:
			nx, ny = x+d[0], y+d[1]
			if nx >= 0 and nx < len(board) and ny >= 0 and ny < len(board[0]):
				if (nx, ny) not in visited:
					next_char = board[nx][ny]
					if next_char in trieNode.children:
						visited.add((nx,ny))
						dfs(nx, ny, trieNode.children[next_char], acc+next_char)
						visited.remove((nx,ny))
	  
	for i in range(len(board)):
		for j in range(len(board[0])):
			if board[i][j] in trie.root.children:
				visited.add((i,j))
				dfs(i, j, trie.root.children[board[i][j]], board[i][j])
				visited.remove((i,j))
	return ans
```
