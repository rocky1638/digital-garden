---
type: leetcode
title: 2021. brightest position on street
tags:
  - sorting
  - line-sweep
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-10-20
---

A perfectly straight street is represented by a number line. The street has street lamp(s) on it and is represented by a 2D integer array `lights`. Each `lights[i] = [positioni, rangei]` indicates that there is a street lamp at position `positioni` that lights up the area from `[positioni - rangei, positioni + rangei]` (**inclusive**).

The **brightness** of a position `p` is defined as the number of street lamp that light up the position `p`.

Given `lights`, return _the **brightest** position on the_ _street. If there are multiple brightest positions, return the **smallest** one._

![[2021-brightest-position-on-street.png]]

## solution

This problem is like a simplified version of [[218-the-skyline-problem]]. We notice that brightnesses will only change at the start or end of a light’s range, so we can just line sweep in sorted order through all these events.

Just like the skyline problem, we make sure we tiebreak sorting to have all starts come before ends, to handle the case above at -1 where two lights are touching on the same point.

```python
def brightestPosition(self, lights: List[List[int]]) -> int:
	START, END = 0, 1
	# convert to events
	events = []
	  
	for mid, reach in lights:
		events.append((mid-reach, START))
		events.append((mid+reach, END))
	events.sort(key=lambda x: (x[0], x[1]))
	  
	res = None
	best = 0
	brightness = 0
	for pos, typ in events:
		if typ == START:
			brightness += 1
			if brightness > best:
				best = brightness
				res = pos
		else:
			brightness -= 1
	return res
```
