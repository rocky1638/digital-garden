---
type: leetcode
title: 273. Integer to English Words
tags:
  - math
  - string
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-01
updated: 2024-09-01
---

Convert a non-negative integer `num` to its English words representation.

## solution

Map one’s and ten’s place words in hashmap. Special case teens (including “Ten”).

Then, break down the word into groups of three numbers because that’s how English works (thousands, millions, billions).

```python
def numberToWords(self, num: int) -> str:
	if num == 0:
		return "Zero"
	  
	num_to_word = {
		1: "One",
		2: "Two",
		3: "Three",
		4: "Four",
		5: "Five",
		6: "Six",
		7: "Seven",
		8: "Eight",
		9: "Nine",
	}
	teens = {
		10: "Ten",
		11: "Eleven",
		12: "Twelve",
		13: "Thirteen",
		14: "Fourteen",
		15: "Fifteen",
		16: "Sixteen",
		17: "Seventeen",
		18: "Eighteen",
		19: "Nineteen",
	}
	tens_to_word = {
		2: "Twenty",
		3: "Thirty",
		4: "Forty",
		5: "Fifty",
		6: "Sixty",
		7: "Seventy",
		8: "Eighty",
		9: "Ninety",
	}

	def group_to_words(num):
		res = []
		tens = num % 100
	  
		# teens edge case
		if tens in teens:
			res.append(teens[tens])
		else:
			if tens > 0 and tens % 10 > 0:
				res.append(num_to_word[tens % 10])
			if tens >= 20:
				res.append(tens_to_word[tens // 10])
	  
		if num >= 100:
			res.append(f"{num_to_word[num // 100]} Hundred")
		return " ".join(res[::-1])
	
	gp = 0
	groups = ["", "Thousand", "Million", "Billion"]
	res = []

	while num > 0:
		group = num % 1000
	  
		if group > 0:
			res.append(f"{group_to_words(group)} {groups[gp]}")
	  
		num //= 1000
		gp += 1
	  
	return " ".join(res[::-1]).strip()
```
