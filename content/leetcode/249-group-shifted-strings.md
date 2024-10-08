---
type: leetcode
title: 249. group shifted strings
tags:
  - hashmap
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-13
updated: 2024-08-13
---

Perform the following shift operations on a string:

- **Right shift**: Replace every letter with the **successive** letter of the English alphabet, where 'z' is replaced by 'a'. For example, `"abc"` can be right-shifted to `"bcd"` or `"xyz"` can be right-shifted to `"yza"`.
- **Left shift**: Replace every letter with the **preceding** letter of the English alphabet, where 'a' is replaced by 'z'. For example, `"bcd"` can be left-shifted to `"abc" or` `"yza"` can be left-shifted to `"xyz"`.

We can keep shifting the string in both directions to form an **endless** **shifting sequence**.

- For example, shift `"abc"` to form the sequence: `... <-> "abc" <-> "bcd" <-> ... <-> "xyz" <-> "yza" <-> ...`. `<-> "zab" <-> "abc" <-> ...`

You are given an array of strings `strings`, group together all `strings[i]` that belong to the same shifting sequence. You may return the answer in **any order**.

## solution

We represent the strings as the differences between the ASCII values of adjacent chars. For example, `abc` becomes `(1, 1)`. The difficulty comes when the rotated string crosses from `z` to `a`. Just realize that if the difference becomes the negative complement of `26`, it’s equivalent (`yza` is `(1, -25)`, which we can simplify to `(1, 1)`).

```python
def groupStrings(self, strings: List[str]) -> List[List[str]]:
	def get_diff_repr(s):
	res = []
	for c1, c2 in zip(s[:-1], s[1:]):
		diff = ord(c2)-ord(c1)
		# normalize to positive side of cycle
		if diff < 0:
			diff = 26+diff
		res.append(diff)
		return tuple(res)
	  
	groups = defaultdict(list)
	  
	for s in strings:
		groups[get_diff_repr(s)].append(s)
	return groups.values()
```
