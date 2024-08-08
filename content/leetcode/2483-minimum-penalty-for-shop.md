---
type: leetcode
title: 2483. minimum penalty for shop
tags:
  - prefix-sums
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2022-12-30
updated: 2024-07-14
---

You are given the customer visit log of a shop represented by a **0-indexed** string `customers` consisting only of characters `'N'` and `'Y'`:

- if the `ith` character is `'Y'`, it means that customers come at the `ith` hour
- whereas `'N'` indicates that no customers come at the `ith` hour.

If the shop closes at the `jth` hour (`0 <= j <= n`), the **penalty** is calculated as follows:

- For every hour when the shop is open and no customers come, the penalty increases by `1`.
- For every hour when the shop is closed and customers come, the penalty increases by `1`.

Return _the **earliest** hour at which the shop must be closed to incur a **minimum** penalty._

**Note** that if a shop closes at the `jth` hour, it means the shop is closed at the hour `j`.

## solution

```python
def bestClosingTime(self, customers: str) -> int:
	counts = Counter(customers)
	n_before, y_after = counts["N"], 0
	best_penalty = n_before
	time_to_close = len(customers)

	for i in reversed(range(len(customers))):
		if customers[i] == "Y":
			y_after += 1
		else:
			n_before -= 1

		penalty_if_close = n_before + y_after
		if penalty_if_close <= best_penalty:
			best_penalty = penalty_if_close
			time_to_close = i
	return time_to_close
```
