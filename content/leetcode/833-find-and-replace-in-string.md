---
type: leetcode
title: 833. find and replace in string
tags: 
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-05-23
---

## solutions

### forward iteration (list of lists)

We go through each replacement, making sure not to directly change the value of `s` while we’re iterating, so we don’t mess up indexing for future changes.

Instead, we use a list to store replaced values, making sure to clear out any value that have been replaced.

```python
def findReplaceString(self, s: str, indices: List[int], sources: List[str], targets: List[str]) -> str:
	modified = list(s)

	for idx, source, target in zip(indices, sources, targets):
		if not s[idx:].startswith(source):
			continue

		modified[idx] = target
		for i in range(idx+1, idx+len(source)):
			modified[i] = ""

	return "".join(modified)
```

### reverse-iteration by index

If we first check validity of replacements, and then iterate backwards through the queries (by index), we can be sure that the changes we make to `s` don’t affect indexing for replacements as we move left.

```python
def findReplaceString(self, s: str, indices: List[int], sources: List[str], targets: List[str]) -> str:
	ans = s
	combined = [
		(idx, source, target) for idx, source, target in zip(
			indices, sources, targets
		)
	]
	combined.sort(key=lambda x: -x[0])
	  
	# clear invalid replacements
	for i, (idx, source, target) in enumerate(combined):
		if ans[idx:idx+len(source)] != source:
			combined[i] = (None, None, None)
	  
	for idx, source, target in combined:
		if idx == None:
			continue
		ans = ans[:idx] + target + ans[idx+len(source):]
	return ans
```
