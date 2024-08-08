---
created_at: 2022-11-21
type: leetcode
title: 981. time based key-value store
aliases: 
difficulty: 🟡
link: https://leetcode.com/problems/time-based-key-value-store/
date: 2022-11-21
updated: 2024-08-07
tags:
  - hashmap
  - binary-search
---

Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.

Implement the `TimeMap` class:

- `TimeMap()` Initializes the object of the data structure.
- `void set(String key, String value, int timestamp)` Stores the key `key` with the value `value` at the given time `timestamp`.
- `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, it returns the value associated with the largest `timestamp_prev`. If there are no values, it returns `""`.

## solution

- we use a [[hashmap]] to store values of every `key`.
- at each index of the hashmap, we keep a sorted [[array]] of `timestamp` and `value`.
- because these arrays are sorted, when we search for timestamps in `get`, we can use [[binary-search]].

```python
class TimeMap:
    def __init__(self):
        self.d = defaultdict(list)

    def set(self, key: str, value: str, timestamp: int) -> None:
        self.d[key].append((timestamp, value))

    def get(self, key: str, timestamp: int) -> str:
        # binary search for most recent timestamp <= requested timestamp
        a = self.d[key]
        l, r = 0, len(a)-1
        
        while l <= r:
            m = (l+r)//2
            
            # found the exact timestamp
            if a[m][0] == timestamp:
                return a[m][1]
            
            # if current timestamp is in the future
            # compared to the requested one
            elif a[m][0] > timestamp:
                r = m - 1
                
            # we found the most recent one that occurred before
            # the requested timestamp
            elif (m+1)==len(a) or a[m+1][0] > timestamp:
                return a[m][1]
            
            # only other case is to look to the right
            else:
                l = m + 1
        return ""
```
