---
type: leetcode
title: 277. find the celebrity
tags:
  - graph
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-27
updated: 2024-09-27
---

Suppose you are at a party with `n` people labeled from `0` to `n - 1` and among them, there may exist one celebrity. The definition of a celebrity is that all the other `n - 1` people know the celebrity, but the celebrity does not know any of them.

Now you want to find out who the celebrity is or verify that there is not one. You are only allowed to ask questions like: "Hi, A. Do you know B?" to get information about whether A knows B. You need to find out the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).

You are given a helper function `bool knows(a, b)` that tells you whether `a` knows `b`. Implement a function `int findCelebrity(n)`. There will be exactly one celebrity if they are at the party.

Return _the celebrity's label if there is a celebrity at the party_. If there is no celebrity, return `-1`.

## solutions

### nested loop (brute force)

For each possible celebrity candidate `i`, we can check every other person `j` to see if `i` doesn’t know `j` and `j` knows `i`.

Break early if these conditions fail.

```java
// O(n^2)
public class Solution extends Relation {
	public int findCelebrity(int n) {
		// check if i is the celebrity
		for (int i = 0; i < n; i++) {
			int good_connections = 0;
		  
			for (int j = 0; j < n; j++) {
				if (i == j) {
					continue;
				}
		  
				// i knows someone, so they
				// can't be the celeb
				if (knows(i, j)) {
					continue;
				}
		  
				// if j doesn't know i,
				// i can't be the celeb
				if (!knows(j, i)) {
					continue;
				}
		  
				good_connections++;
			}
		
			if (good_connections == (n-1)) {
				return i;
			}
		}
		return -1;
	}
}
```

### optimized loop

Instead of doing a full nested loop, we can break the problem down into three steps:

1. First, start with a celebrity candidate `celeb` set as 0. For every other person $[1,n]$, check if `celeb` knows them. If they do, then `celeb` is an invalid candidate.

The crux here is that we are allowed to advance `celeb` to `i`, skipping the values in between. This is because we initially skipped those in-between values because `celeb` didn’t know them, and this means that they can’t possibly be the celebrity!

2. Once we have our _only_ possible celebrity candidate, we need to check the people less than `celeb` to make sure `celeb` doesn’t know them. We didn’t check this in the first loop.
3. Finally, we need to confirm that everyone knows `celeb`. So far, we’ve only checked that `celeb` doesn’t know anyone.

If these checks all pass, then `celeb` is the celebrity!

```java
public class Solution extends Relation {
	public int findCelebrity(int n) {
		int celeb = 0;
		  
		for (int i = 1; i < n; i++) {
			// if celeb knows i, celeb is invalid
			// make i new celeb candidate
			if (knows(celeb, i)) {
				celeb = i;
			}
		}
		  
		// we already know that celeb doesn't know
		// anyone greater than them (from above)
		for (int i = 0; i < celeb; i++) {
			if (knows(celeb, i)) {
				return -1;
			}
		}
		  
		// everyone needs to know celeb
		for (int i = 0; i < n; i++) {
			if (!knows(i, celeb)) {
				return -1;
			}
		}
		  
		return celeb;
	}
}
```
