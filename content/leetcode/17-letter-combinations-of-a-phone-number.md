---
created_at: 2022-11-22
type: leetcode
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/letter-combinations-of-a-phone-number/
date: 2022-11-22
updated: 2024-09-03
---

# 17. Letter Combinations of a Phone Number

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []
        
        d = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z']
        }
        
        ans = [""]
        for digit in digits:
            next_level = []
            for char in d[digit]:
                for partial in ans:
                    next_level.append(partial+char)
            ans = next_level[:]
        return ans
```

- for each number in `digits`, the number of possibilities grows exponentially.
	- so, runtime is $O(3^n)$ approximately where $n$ is the length of `digits`.
- we work through each digit, and for each new digit, we append each possible character for that `digit` to each existing partial solution.

Categories:: [[hashmap]], [[string]], [[backtracking]]
