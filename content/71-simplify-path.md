---
type: leetcode
title: 71. simplify path
tags:
  - string
  - stack
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-28
updated: 2024-08-28
---

Given an absolute path for a Unix-style file system, which begins with a slash `'/'`, transform this path into its **simplified canonical path**.

In Unix-style file system context, a single period `'.'` signifies the current directory, a double period `".."` denotes moving up one directory level, and multiple slashes such as `"//"` are interpreted as a single slash. In this problem, treat sequences of periods not covered by the previous rules (like `"..."`) as valid names for files or directories.

The simplified canonical path should adhere to the following rules:

- It must start with a single slash `'/'`.
- Directories within the path should be separated by only one slash `'/'`.
- It should not end with a slash `'/'`, unless it's the root directory.
- It should exclude any single or double periods used to denote current or parent directories.

Return the new path.

## solution

Pretty simply string manipulation and stack question. Kind of like a simpler [[1472-design-browser-history]].

```python
def simplifyPath(self, path: str) -> str:
	# 1. split path on /, remove unnecessary slashes
	# 2. handle ".."
	# 3. handle root directory special case
	  
	path_parts = path.split("/")
	  
	stack = []
	for part in path_parts:
		if len(part) == 0: continue
		if part == ".": continue
		if part == "..":
			if len(stack) == 0:
				continue
			stack.pop()
		else:
			stack.append(part)

	# special case for root
	if len(stack) == 0:
		return "/"
	return "/" + "/".join(stack)
```
