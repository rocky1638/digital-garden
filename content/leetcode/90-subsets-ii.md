---
type: leetcode
title: 90. subsets ii
aliases: []
difficulty: 🟡
link: https://leetcode.com/problems/subsets-ii
date: 2023-01-10
updated: 2024-09-02
---

Given an integer array `nums` that may contain duplicates, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

## Using extra space.

- we use a set here to remember the subsets that we’ve seen already.
- we sort because leetcode expects the actual subsets to be in order.

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        ans = [[]]
        seen = set()
        nums.sort()
        
        def backtrack(idx, acc):
            if idx < len(nums):
                # don't take the current number
                backtrack(idx+1, acc)
                # take the current number
                backtrack(idx+1, acc[:]+[nums[idx]])

                new = "".join(map(str, acc[:]+[nums[idx]]))
                if new not in seen:
                    ans.append(acc[:]+[nums[idx]])
                    seen.add(new)
            
        backtrack(0, [])
        return ans
```

## Without extra space.

Instead of keeping a set to store what we’ve seen, we just store the duplicates in “blocks”, and then we can recurse on every possible number of them at once instead of risking the chance of using the same number of a duplicate in two recursive branches.

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        """
        - the only way we get duplicates are when there are multiples
          of the same number, and we can pick some of them.
        - if we sort the array, we can think of these duplicates as blocks.
        - then, in one recursive iteration, we can pick 0-n of these
          duplicates in a block and recurse.
        """

        ans = [[]]
        nums.sort()

        blocks = []
        cur = None 
        for num in nums:
            if cur is None:
                cur = num
                count = 1
            elif cur == num:
                count += 1
            else:
                blocks.append((cur, count))
                cur = num
                count = 1
        blocks.append((cur, count)) 
        
        def backtrack(idx, acc):
            if idx < len(blocks):
                val, count = blocks[idx]
                for cnt in range(count+1):
                    # take the current number cnt times
                    backtrack(idx+1, acc[:]+cnt*[val])
                    if cnt > 0:
                        ans.append(acc[:]+cnt*[val])
            
        backtrack(0, [])
        return ans
```

Here’s another elegant way to do it without the block construction.

The way we append “intermediate” values of `acc` to our `res` kind of reminds me of [[254-factor-combinations]].

```python
def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
	nums.sort()
	res = []
	acc = []

	# recursive call tries to fill the current idx in subset
	# with every distinct value...
	def recurse(idx):
		res.append(acc[:])
	  
		for i in range(idx, len(nums)):
			# this is why we skip duplicates
			if i > idx and nums[i] == nums[i-1]:
				continue
			acc.append(nums[i])
			recurse(i+1)
			acc.pop()
	  
	recurse(0)
	return res
```
