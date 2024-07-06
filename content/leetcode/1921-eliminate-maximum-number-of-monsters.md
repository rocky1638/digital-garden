---
type: leetcode
title: 1921. eliminate maximum number of monsters
tags:
  - sorting
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-19
---


You are playing a video game where you are defending your city from a group of `n` monsters. You are given a **0-indexed** integer array `dist` of size `n`, where `dist[i]` is the **initial distance** in kilometers of the `ith` monster from the city.

The monsters walk toward the city at a **constant** speed. The speed of each monster is given to you in an integer array `speed` of size `n`, where `speed[i]` is the speed of the `ith` monster in kilometers per minute.

You have a weapon that, once fully charged, can eliminate a **single** monster. However, the weapon takes **one minute** to charge. The weapon is fully charged at the very start.

You lose when any monster reaches your city. If a monster reaches the city at the exact moment the weapon is fully charged, it counts as a **loss**, and the game ends before you can use your weapon.

Return _the **maximum** number of monsters that you can eliminate before you lose, or_ `n` _if you can eliminate all the monsters before they reach the city._

## solution

We just want to order the monsters by the time that they will arrive at our city. If any two arrive at the same time, then we won’t have time to reload and kill the monster.

So, we can just create a sorted array based on arrival times, and simulate shooting one of the monsters at each time slot.

```python
def eliminateMaximum(self, dist: List[int], speed: List[int]) -> int:
	t = [math.ceil(d/s) for d, s in zip(dist, speed)]
	# sorted by timestamp of arrival
	t.sort()
	
	ans = 0
	elapsed = 0
	for arrival in t:
		if arrival - elapsed > 0:
			ans += 1
			elapsed += 1
		else:
			return ans 
	
	return ans
