---
type: leetcode
title: 648. replace words
tags:
  - trie
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-18
updated: 2024-08-18
---

In English, we have a concept called **root**, which can be followed by some other word to form another longer word - let's call this word **derivative**. For example, when the **root** `"help"` is followed by the word `"ful"`, we can form a derivative `"helpful"`.

Given a `dictionary` consisting of many **roots** and a `sentence` consisting of words separated by spaces, replace all the derivatives in the sentence with the **root** forming it. If a derivative can be replaced by more than one **root**, replace it with the **root** that has **the shortest length**.

Return _the `sentence`_ after the replacement.

## solution

Make a trie, and then search for the prefix of each of the sentence words, return the shortest one found.

```python
class TrieNode:
	def __init__(self, char, is_end):
		self.char = char
		self.children = {}
		self.is_end = is_end

	def __str__(self):
		return f"({self.char}) {self.children.keys()} {self.is_end}"
  
class Trie:
	def __init__(self):
		self.root = TrieNode(None, False)

	def add_word(self, word):
		cur = self.root
		for i, c in enumerate(word):
			if c not in cur.children:
				cur.children[c] = TrieNode(c, i == len(word)-1)
				cur = cur.children[c]
		cur.is_end = True

	def search_for_prefix(self, word):
		cur = self.root
		for i, c in enumerate(word):
			if cur.is_end:
				return word[:i]
			if c in cur.children:
				cur = cur.children[c]
			else:
			break
		return ""
  
class Solution:
	def replaceWords(self, dictionary: List[str], sentence: str) -> str:
		trie = Trie()
		for word in dictionary:
			trie.add_word(word)
		  
		sentence_words = []
		for word in sentence.split(" "):
			prefix = trie.search_for_prefix(word)
			sentence_words.append(prefix if prefix else word)
		return " ".join(sentence_words)
```
