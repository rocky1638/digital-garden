# 252. Meeting Rooms

```python
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        s = sorted(intervals, key=lambda x: x[0])
        
        for m1, m2 in zip(s[:-1], s[1:]):
            # if first meeting ends after second meeting starts
            if m1[1] > m2[0]:
                return False
        return True
```

- sort the [[intervals|intervals]] by start time.
- if any meeting ends after the next one starts, we have a conflict.

[[sorting]]