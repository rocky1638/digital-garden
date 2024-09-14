---
type: leetcode
title: 68. text justification
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-27
updated: 2024-08-27
---

Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

**Note:**

- A word is defined as a character sequence consisting of non-space characters only.
- Each word's length is guaranteed to be greater than `0` and not exceed `maxWidth`.
- The input array `words` contains at least one word.

## solution

This is pretty straightforward, just implement the thing.

First, we split the text into lines based on requiring at least one space between adjacent words.

```python
def splitIntoLines(self, words, maxWidth):
	lines = []
	line_words = []
	remaining_len = maxWidth

	for word in words:
		if remaining_len == maxWidth:
			line_words.append(word)
			remaining_len -= len(word)
		else:
			if remaining_len - len(word) > 0: # account for space
				line_words.append(word)
				remaining_len -= len(word)+1
			else:
				lines.append(line_words[:])
				line_words = [word]
				remaining_len = maxWidth - len(word)

	if line_words:
		lines.append(line_words[:])

	return lines
```

Then for each line, format it with correct spacing, accounting for ending line/single-word lines.

```python
def formatLine(self, line, maxWidth, is_last):
	total_word_len = sum([len(word) for word in line])
	required_spaces = len(line)-1
	extra_spaces = maxWidth - total_word_len - required_spaces
	  
	if is_last or len(line) == 1:
		return " ".join(line) + " "*extra_spaces

	extra_spaces_per_word = extra_spaces // required_spaces
	remainder = extra_spaces % required_spaces
	res = []
	for i, word in enumerate(line):
		res.append(word)
	  
		if i != len(line)-1:
			res.append(" "*(extra_spaces_per_word+1))
	  
		if remainder > 0:
			res.append(" ")
			remainder -= 1

	return "".join(res)
```

Then, just put it all together.

```python
def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
	lines = self.splitIntoLines(words, maxWidth)
  
	res = []
	formatted_line = []
	for i, line in enumerate(lines):
		res.append(
			self.formatLine(line, maxWidth, is_last=i==len(lines)-1)
		)
	return res
```
