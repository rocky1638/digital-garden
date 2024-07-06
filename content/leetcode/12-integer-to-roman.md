---
type: leetcode
title: 12. integer to roman
tags:
  - hashmap
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-06-19
---

Seven different symbols represent Roman numerals with the following values:

|Symbol|Value|
|---|---|
|I|1|
|V|5|
|X|10|
|L|50|
|C|100|
|D|500|
|M|1000|

Roman numerals are formed by appending the conversions of decimal place values from highest to lowest. Converting a decimal place value into a Roman numeral has the following rules:

- If the value does not start with 4 or 9, select the symbol of the maximal value that can be subtracted from the input, append that symbol to the result, subtract its value, and convert the remainder to a Roman numeral.
- If the value starts with 4 or 9 use the **subtractive form** representing one symbol subtracted from the following symbol, for example, 4 is 1 (`I`) less than 5 (`V`): `IV` and 9 is 1 (`I`) less than 10 (`X`): `IX`. Only the following subtractive forms are used: 4 (`IV`), 9 (`IX`), 40 (`XL`), 90 (`XC`), 400 (`CD`) and 900 (`CM`).
- Only powers of 10 (`I`, `X`, `C`, `M`) can be appended consecutively at most 3 times to represent multiples of 10. You cannot append 5 (`V`), 50 (`L`), or 500 (`D`) multiple times. If you need to append a symbol 4 times use the **subtractive form**.

Given an integer, convert it to a Roman numeral.

## solution

We iteratively build up the roman numeral representation by going from largest valued letter downwards. We have special cases in the dictionary for 4, 9, 40, 90, etc.

```python
def intToRoman(self, num: int) -> str:
	d = [
	(1, "I"),
	(4, "IV"),
	(5, "V"),
	(9, "IX"),
	(10, "X"),
	(40, "XL"),
	(50, "L"),
	(90, "XC"),
	(100, "C"),
	(400, "CD"),
	(500, "D"),
	(900, "CM"),
	(1000, "M")
	]
	  
	idx = len(d)-1
	ans = ""
	while num > 0:
		if d[idx][0] > num:
			idx -= 1
		elif d[idx][0] <= num:
			ans += d[idx][1]
			num -= d[idx][0]
	return ans
```
