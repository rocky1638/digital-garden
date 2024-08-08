---
type: leetcode
title: 424. longest repeating character replacement
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/longest-repeating-character-replacement/
date: 2022-12-21
updated: 2024-08-07
---

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return _the length of the longest substring containing the same letter you can get after performing the above operations_.

## solution

We use a sliding window approach. Keep track of the frequency of characters in our window with a frequency map.
The main intuition is that at every character, we have to consider the _most common character_ as the main character. If after choosing our main character, there are more than `k` other characters in the window, we slide the left pointer up until there are less than `k` other characters.

Note that the “main" character may change during this process, so we have to update our “main” character after each removal from the left and addition from the right.

```python
def characterReplacement(self, s: str, k: int) -> int:
	ans = 0
	char_counts = Counter()
	mc = None
	l = 0
	  
	for r in range(len(s)):
		c = s[r]
		char_counts[c] += 1
	  
		mc = char_counts.most_common()[0][0]

		while (r-l+1) - char_counts[mc] > k:
			char_counts[s[l]] -= 1
			mc = char_counts.most_common()[0][0]
			l += 1
	  
		ans = max(ans, r-l+1)
	return ans
```

Instead of using a counter and calling an $O(26)$ `most_common` function every iteration, we can instead just keep track of the frequency of the highest character (note that we don’t actually care what the character’s value is).

```python
def characterReplacement(self, s: str, k: int) -> int:
	freqMap = defaultdict(int)
	l = 0
	maxFreq = 0

	for r in range(len(s)):
		freqMap[s[r]] += 1
		maxFreq = max(maxFreq, freqMap[s[r]])

		if r - l + 1 - maxFreq > k:
			freqMap[s[l]] -= 1
			maxFreq = max(freqMap.values())
			l += 1

	return r - l + 1
```
