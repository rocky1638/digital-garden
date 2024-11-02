---
type: leetcode
title: 1233. remove sub-folders from the filesystem
tags:
  - trie
  - sorting
  - dfs
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-22
updated: 2024-10-22
---

Given a list of folders `folder`, return _the folders after removing all **sub-folders** in those folders_. You may return the answer in **any order**.

If a `folder[i]` is located within another `folder[j]`, it is called a **sub-folder** of it. A sub-folder of `folder[j]` must start with `folder[j]`, followed by a `"/"`. For example, `"/a/b"` is a sub-folder of `"/a"`, but `"/b"` is not a sub-folder of `"/a/b/c"`.

The format of a path is one or more concatenated strings of the form: `'/'` followed by one or more lowercase English letters.

- For example, `"/leetcode"` and `"/leetcode/problems"` are valid paths while an empty string and `"/"` are not.

## solutions

### trie + break early on insertion

We break early on insertion and return `False` if during insertion we hit an ending node, meaning that a parent folder has already been seen.

Note that we need to first sort lexicographically for this to work.

```python
class TrieNode:
	def __init__(self, val=None, is_end=False):
		self.val = val
		self.is_end = False
		self.children = {}
    
class Trie:
	def __init__(self):
		self.root = TrieNode()
	
	def insert(self, parts: list[str]):
		cur = self.root
		for part in parts:
			if part in cur.children:
				if cur.children[part].is_end:
					return False
				cur = cur.children[part]
			else: # new TrieNode
				new_node = TrieNode(part)
				cur.children[part] = (new_node)
				cur = new_node
		cur.is_end = True
	return True

def removeSubfolders(self, folder: List[str]) -> List[str]:
	res = []
	t = Trie()
	folder.sort()

	for path in folder:
		parts = path.split("/")
		if t.insert(parts):
			res.append(path)
	return res
```

### trie + break early on collection/traversal

We can insert all paths into the trie, and then DFS the trie, but break whenever we hit a node marked as `is_end`, as every further traversal would be a sub-folder.

```python
class TrieNode:
	def __init__(self, val=None, is_end=False):
		self.val = val
		self.is_end = False
		self.children = {}

class Trie:
	def __init__(self):
		self.root = TrieNode()

	def insert(self, parts: list[str]):
		cur = self.root
		for part in parts:
			if part not in cur.children:
				new_node = TrieNode(part)
				cur.children[part] = new_node
			cur = cur.children[part]
		cur.is_end = True

	def collect(self, root: TrieNode):
		parents = []
		acc = []
		def _helper(node):
			if not node:
				return
	  
			# first ending node is parent
			# all further traversal would give subfolders
			if node.is_end:
				parents.append("/".join(acc))
				return
	  
			for child_key in node.children:
				acc.append(node.children[child_key].val)
				_helper(node.children[child_key])
				acc.pop()

		_helper(root)
		return parents
	  
def removeSubfolders(self, folder: List[str]) -> List[str]:
	res = []
	t = Trie()
	for path in folder:
		parts = path.split("/")
		t.insert(parts)
	return t.collect(t.root)
```
