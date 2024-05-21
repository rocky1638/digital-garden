---
type: leetcode
title: "716. max stack"
date: 2022-11-30
updated: 2024-05-20
---

```python
from sortedcontainers import SortedList

class MaxStack:

    def __init__(self):
        self.stack = SortedList()
        self.values = SortedList()
        self.cnt = 0

    def push(self, x: int) -> None:
        self.stack.add((self.cnt, x))
        self.values.add((x, self.cnt))
        self.cnt += 1

    def pop(self) -> int:
        idx, val = self.stack.pop()
        self.values.remove((val, idx))
        return val

    def top(self) -> int:
        return self.stack[-1][1]

    def peekMax(self) -> int:
        return self.values[-1][0]

    def popMax(self) -> int:
        val, idx = self.values.pop()
        self.stack.remove((idx, val))
        return val
```

- key insight is that we want to maintain two “sorted” arrays, one in push order and one in value order.
- `pop` and `top` come from the push order list.
- `peekMax` and `popMax` come from the value order list.
- `SortedList` automatically supports $O(\log(n))$ insertion, lookup, and removal.

[[sorting]], [[array]], [[stack]]
