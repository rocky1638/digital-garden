---
type: leetcode
title: 408. valid word abbreviation
tags:
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-10
updated: 2024-07-10
---

A string can be **abbreviated** by replacing any number of **non-adjacent**, **non-empty** substrings with their lengths. The lengths **should not** have leading zeros.

For example, a string such as `"substitution"` could be abbreviated as (but not limited to):

- `"s10n"` (`"s ubstitutio n"`)
- `"sub4u4"` (`"sub stit u tion"`)
- `"12"` (`"substitution"`)
- `"su3i1u2on"` (`"su bst i t u ti on"`)
- `"substitution"` (no substrings replaced)

The following are **not valid** abbreviations:

- `"s55n"` (`"s ubsti tutio n"`, the replaced substrings are adjacent)
- `"s010n"` (has leading zeros)
- `"s0ubstitution"` (replaces an empty substring)

Given a string `word` and an abbreviation `abbr`, return _whether the string **matches** the given abbreviation_.

A **substring** is a contiguous **non-empty** sequence of characters within a string.

## solution

Iterate through the two strings.

```python
def validWordAbbreviation(self, word: str, abbr: str) -> bool:
	word_ptr, abbr_ptr = 0, 0

	while abbr_ptr < len(abbr) and word_ptr < len(word):
		# check for character match
		if abbr[abbr_ptr].isalpha():
			if word[word_ptr] != abbr[abbr_ptr]:
				return False
			abbr_ptr += 1
			word_ptr += 1

		else:
			# parse the number
			num = int(abbr[abbr_ptr])
			if num == 0: return False
			abbr_ptr += 1
			while abbr_ptr < len(abbr) and abbr[abbr_ptr].isnumeric():
				num *= 10
				num += int(abbr[abbr_ptr])
				abbr_ptr += 1
			word_ptr += num

	return abbr_ptr == len(abbr) and word_ptr == len(word)
```
