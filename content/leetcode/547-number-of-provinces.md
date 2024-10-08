---
type: leetcode
title: 547. number of provinces
tags:
  - dfs
  - union-find
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-02
updated: 2024-10-02
---

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return _the total number of **provinces**_.

## solutions

### dfs

Maintain a seen set, and just DFS whenever we see a new node, which is basically just the solution to [[200-number-of-islands]].

```java
// O(n^2)
class Solution {
	public void dfs(int[][] isConnected, HashSet<Integer> seen, int x) {
		for (int i = 0; i < isConnected.length; i++) {
			if (isConnected[x][i] == 1 && !seen.contains(i)) {
				seen.add(i);
				dfs(isConnected, seen, i);
			}
		}
	}

	public int findCircleNum(int[][] isConnected) {
		HashSet<Integer> seen = new HashSet<Integer>();
		int res = 0;
		for (int x = 0; x < isConnected.length; x++) {
			if (!seen.contains(x)) {
				seen.add(x);
				dfs(isConnected, seen, x);
				res += 1;
			}
		}
		return res;
	}
}
```

### union-find

Standard union-find. To avoid doing an extra $O(n)$ recursion on the parents, just maintain a running counter of how many components are remaining (and reduce by 1 after every successful `union` operation).

```java
// O(n^2)
class UnionFind {  
    public ArrayList<Integer> parents;  
    public ArrayList<Integer> sizes;  
  
    public UnionFind(int n) {  
        parents = new ArrayList<>();  
        sizes = new ArrayList<>();  
        for (int i = 0; i < n; i++) {  
            parents.add(i);  
            sizes.add(1);  
        }  
    }  
  
    public boolean union(int u, int v) {  
        int pu = find(u);  // Find root of u  
        int pv = find(v);  // Find root of v  
  
        if (pu == pv) {  
            return false;  // u and v are already in the same set  
        }  
  
        // Union by size: attach the smaller tree to the larger one  
        if (sizes.get(pu) < sizes.get(pv)) {  
            parents.set(pu, pv);  // Attach smaller tree pu to larger tree pv  
            sizes.set(pv, sizes.get(pv) + sizes.get(pu));  // Update size of pv's tree  
        } else {  
            parents.set(pv, pu);  // Attach smaller tree pv to larger tree pu  
            sizes.set(pu, sizes.get(pu) + sizes.get(pv));  // Update size of pu's tree  
        }  
  
        return true;  
    }  
  
    public int find(int u) {  
        if (u != parents.get(u)) {  
            // Path compression step  
            parents.set(u, find(parents.get(u)));  
        }  
        return parents.get(u);  
    }  
}

class Solution {  
    public int findCircleNum(int[][] isConnected) {  
        int n = isConnected.length;  
        int res = n;  
        UnionFind uf = new UnionFind(n);  
        for (int i = 0; i < n; i++) {  
            for (int j = 0; j < n; j++) {  
                if (isConnected[i][j] == 1 && uf.union(i, j)) {  
                    res--;  
                }  
            }  
        }  
        return res;  
    }  
}
```
