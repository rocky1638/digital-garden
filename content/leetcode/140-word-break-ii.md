---
type: leetcode
title: 140. word break ii
aliases: 
tags:
  - recursion
  - memoization
  - backtracking
difficulty: 🔴
link: https://leetcode.com/problems/word-break-ii/
date: 2022-11-17
updated: 2024-08-17
---

Given a string `s` and a dictionary of strings `wordDict`, add spaces in `s` to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in **any order**.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

## solutions

### recursion

Below are two options for doing the recursion for this problem. The first one here loops through all the possible valid next words during each recursive call.

```python
def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
	wordSet = set(wordDict)
	ans = []
	
	def recurse(i, acc):
		if i == len(s):
			ans.append(acc)
			return
	
		string = ""
		while i < len(s):
			string += s[i]
			if string in wordSet:
				if len(acc) == 0:
					recurse(i+1, string)
				else:
					recurse(i+1, acc+" "+string)
			i += 1
	
	recurse(0, "")
	return ans
```

This second one instead maintains a pointer to the start of the currently tracked window in the recursion parameters, and if the current window is valid, recurses on a new window.

```python
def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
	word_set = set(wordDict)
	acc = []
	sentence = []
	  
	def recurse(idx, wl):
		if idx == len(s) and wl == len(s):
			acc.append(" ".join(sentence))
			return
		if idx == len(s) or wl == len(s):
			return
		window_word = s[wl:idx+1]
		if window_word in word_set:
			sentence.append(window_word)
			recurse(idx+1, idx+1)
			sentence.pop()
		recurse(idx+1, wl)
	  
	recurse(0, 0)
	return acc
```

### memoization

I didn’t write out this solution, but it makes sense to me that we could somehow tabulate all of the valid solutions for subproblems by iterating from the end of the string `s`.

Starting from `s[-1]`, we move backwards until `s[i:]` is in `wordDict`. So, `dp[i]` contains the valid word. Skipping ahead, so we are at some other index `i`. We iterate from `i` forwards, trying to form valid words. When we find a valid word `s[i:j]`, we check `dp[j]` to see what sentences are valid starting at `j`, then add `s[i:j]` to each of those sentences, pushing these new longer sentences starting at `i` into `dp[i]`.

Here’s an example of this concept, using recursion:

```python
def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
	word_set = set(wordDict)
	memo = {}
	  
	def dfs(remaining_str):
		if remaining_str in memo:
			return memo[remaining_str]

		if not remaining_str:
			return [""]
		  
		results = []
		for i in range(1, len(remaining_str) + 1):
			current_word = remaining_str[:i]
			# If the current substring is a valid word
			if current_word in word_set:
				following_sentences = dfs(remaining_str[i:])
				for following_sentence in following_sentences:
					results.append(
						current_word + (" " if following_sentence else "") + following_sentence
					)
		# Memoize the results for the current substring
		memo[remaining_str] = results
		return results
	return dfs(s)
```
