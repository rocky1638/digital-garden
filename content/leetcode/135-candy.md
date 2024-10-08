---
type: leetcode
title: 135. candy
tags:
  - simulation
  - greedy
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-03
updated: 2024-10-03
---

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

Return _the minimum number of candies you need to have to distribute the candies to the children_.

## solution

This one is pretty cool, and the intuition starts off with a basic idea: to minimize how much candy we give out, we should give kids only one candy whenever you’re allowed to.

The only kids we can give one candy to are the ones who are in “valleys”. Then, to optimize, we should expand outwards/upwards from those valleys, increasing the candies by one each time.

With this intuition, we can write the implementation. Note that if we visit a child that’s already been visited by another outwards expansion, if our current candy value is higher, we have to take the higher value.

```python
def candy(self, ratings: List[int]) -> int:  
	"""  
	- Set candies in every "valley" to 1  
	- Expand outwards from every valley while increasing  
	- If we reach a kid while expanding outwards that's already  
	been reached, we need to use the new bigger value  
	
	1 <- 0 -> 2 -> 3 <- 2 -> 9 <- 1  
	2    1    2    3    1    2    1  
	"""  
	candies = [0]*len(ratings)  
	
	def expand_outwards(x):  
		candies[x] = 1  
	
		nex = 2  
		l = x-1  
		# while increasing going left  
		while l >= 0 and ratings[l] > ratings[l+1]:  
			candies[l] = max(candies[l], nex)  
			nex += 1  
			l -= 1  

		nex = 2  
		r = x+1  
		# while increasing going right  
		while r < len(ratings) and ratings[r] > ratings[r-1]:  
			candies[r] = max(candies[r], nex)  
			nex += 1  
			r += 1  
	
	starting_points = []  
	for x in range(len(ratings)):  
		if ( # valley  
			(x == 0 or ratings[x-1] >= ratings[x])  
			and (x == len(ratings)-1 or ratings[x+1] >= ratings[x])   
		):  
			starting_points.append(x)  
	
	for kid in starting_points:  
		expand_outwards(kid)  
	
	return sum(candies)
```
