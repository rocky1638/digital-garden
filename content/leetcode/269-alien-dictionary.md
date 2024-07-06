---
type: leetcode
title: 269. alien dictionary
tags:
  - topological-sort
  - graph
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-04
---

There is a new alien language that uses the English alphabet. However, the order of the letters is unknown to you.

You are given a list of strings `words` from the alien language's dictionary. Now it is claimed that the strings in `words` are sorted lexicographically by the rules of this new language.

If this claim is incorrect, and the given arrangement of string in `words` cannot correspond to any order of letters, return `"".`

Otherwise, return _a string of the unique letters in the new alien language sorted in **lexicographically increasing order** by the new language's rules__._ If there are multiple solutions, return _**any of them**_.

## solution

```python
def _findConnection(self, word1, word2):
	for i in range(min(len(word1), len(word2))):
		if word1[i] != word2[i]:
			return (word1[i], word2[i])
	if len(word2) < len(word1):
		return False
	return None
  

def alienOrder(self, words: List[str]) -> str:
	if len(words) == 1:
		return "".join(list(set(words[0])))
	  
	# directed graph where u -> v means u comes before v
	g = defaultdict(list)
	indegrees = Counter()
	nodes = set()

	# construct graph, and catch "abc, ab" edge case
	for word1, word2 in zip(words[:-1], words[1:]):
		nodes.update(word1)
		nodes.update(word2)
		edge = self._findConnection(word1, word2)
		if edge is False:
			return ""
		if edge is not None:
			g[edge[0]].append(edge[1])
			indegrees[edge[1]] += 1

	# initialize topsort
	q = deque()
	topsort = []
	for node in list(nodes):
		if indegrees[node] == 0:
			q.append(node)

	# perform topsort
	while q:
		cur = q.popleft()
		topsort.append(cur)
		for neighbor in g[cur]:
			indegrees[neighbor] -= 1
			if indegrees[neighbor] == 0:
				q.append(neighbor)
	  
	if len(topsort) == len(nodes):
		return "".join(topsort)
	return ""
```
