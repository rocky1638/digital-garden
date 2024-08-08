---
type: leetcode
title: 1650. lowest common ancestor of a binary tree iii
tags:
  - linked-list
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-07-10
updated: 2024-07-10
---


Given two nodes of a binary tree `p` and `q`, return _their lowest common ancestor (LCA)_.

Each node will have a reference to its parent node. The definition for `Node` is below:

```python
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node parent;
}

```

According to the **[definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor)**: "The lowest common ancestor of two nodes p and q in a tree T is the lowest node that has both p and q as descendants (where we allow **a node to be a descendant of itself**)."

## solutions

### set

Just find all of the ancestors for `p`, and then return the first match when finding the parents of `q`.

```python
def lowestCommonAncestor(self, p: 'Node', q: 'Node') -> 'Node':
	p_ancestors = set([p])

	while p.parent:
		p = p.parent
		p_ancestors.add(p)
	  
	while q:
		if q in p_ancestors:
			return q
		q = q.parent
```

### constant space

This is a big brain solution that works by realizing that if, whenever we reach root node on one of the paths, we can move our pointer to the start of the other path. Imagine the following generalized scenario.

```
P: p1 -> p2 -> p3 -> c1 -> c2 -> c3  
Q: q1 -> c1 -> c2 -> c3
```

The idea is that by concatenating the paths of P and Q, resulting in:

```
P -> Q: (p1 -> p2 -> p3 -> c1 -> c2 -> c3)-> (q1 -> c1 -> c2 -> c3)  
Q -> P: (q1 -> c1 -> c2 -> c3) -> (p1 -> p2 -> p3 -> c1 -> c2 -> c3)  
```

You can see the length of P -> Q is equal to Q -> P and they both end at c3.

Given the fact that there is a common path at the end of P -> Q and Q -> P which is c1 -> c2 -> c3, this guarantees that these two paths P -> Q and Q -> P with definitely reach a common node in somewhere, and the first encountered common node is the LCA.

```python
def lowestCommonAncestor(self, p: 'Node', q: 'Node') -> 'Node':
	p1, p2 = p, q
	while p1 != p2:
		p1 = p1.parent if p1.parent else q
		p2 = p2.parent if p2.parent else p
	
	return p1
```
