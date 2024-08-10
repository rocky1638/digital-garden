---
type: leetcode
title: 2468. split message based on limit
tags:
  - math
  - string
  - a
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-10
updated: 2024-08-10
---

You are given a string, `message`, and a positive integer, `limit`.

You must **split** `message` into one or more **parts** based on `limit`. Each resulting part should have the suffix `"<a/b>"`, where `"b"` is to be **replaced** with the total number of parts and `"a"` is to be **replaced** with the index of the part, starting from `1` and going up to `b`. Additionally, the length of each resulting part (including its suffix) should be **equal** to `limit`, except for the last part whose length can be **at most** `limit`.

The resulting parts should be formed such that when their suffixes are removed and they are all concatenated **in order**, they should be equal to `message`. Also, the result should contain as few parts as possible.

Return _the parts_ `message` _would be split into as an array of strings_. If it is impossible to split `message` as required, return _an empty array_.

## solution

This question feels very overwhelming at first. To think that the values are all shifting under you as you try to choose a value for the number of parts $k$…

Some ideas that help to make it easier to reason about:

- The length of the metadata (`<part/total_parts>`) only grows in length exponentially. For example, the length of this value only really increases after 10, 100, etc.
	- Because of this, as we increase $k$, we should be, for all except the boundary values of 10, 100, will be shortening the length of each part.
- Instead of overthinking it, we can just start $k$ from $1$ and increment it until we can fit all the parts.

How do we write the condition to check that our choice of $k$ is valid? The key here is to break down the entire string by parts, and not just each part. For example, instead of thinking of the length of each part and trying to sum them, just compare the total sum of the parts with the maximum limit that we can use.

In the case of this problem, the maximum length of the formatted string is `limit * k`. Then, for the candidate string with $k$, we know the sum is `sum(len of numerators) + len(message) + 3k + len(denominator)*k`, where $3k$ is the `</>` string. After realizing this, we see the added benefit of gradually increasing $k$ in our search -- we can keep a running accumulator `numerator_len_acc` of the total lengths of all of the numerators.

Finally, we also need to consider the case where there is no valid $k$. We can break early if the string `<parts/parts>` exceeds `limit`.

Once $k$ is solved for, just construct the parts logically.

```python
def splitMessage(self, message: str, limit: int) -> List[str]:
	n = len(message)
	numerator_len_acc = 0
	k = 0
	# gradually step up k until the split will work
	# example; limit=9
	# k == 0
	# 0 + message + </>*0 > limit * 0 -> True, continue (empty case)
	# k == 1
	# 1 + message + </>*1 + 1*1 > limit*1
	# k == 2
	# len("1" + "2") + message + </>*2 + len("2")*2 > limit*2
	while numerator_len_acc + n + (3+len(str(k)))*k > limit*k:
		# <k/k> already takes limit, so trying to
		# go higher won't help...
		if 3 + len(str(k)) * 2 >= limit:
			return []
	  
	k += 1
		numerator_len_acc += len(str(k))
	res = []
	message_ptr = 0
	for j in range(1, k+1):
		part_len = limit - (len(str(j))+3+len(str(k)))
		res.append(f"{message[message_ptr:message_ptr+part_len]}<{j}/{k}>")
		message_ptr += part_len
	return res
```
