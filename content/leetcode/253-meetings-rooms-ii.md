# 253. Meeting Rooms II

```python
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        # sort by start time
        sa = sorted(intervals, key=lambda x: x[0])
        
        # keep track of answer
        max_rooms = 1
        
        # keep a min-heap of active rooms, and when they end
        # room with earliest ending meeting is at the top of the heap
        active_rooms = [sa[0][1]]
        heapq.heapify(active_rooms)
        
        for s, e in sa[1:]:
            # we need another room
            if s < active_rooms[0]:
                heapq.heappush(active_rooms, e)
                max_rooms = max(max_rooms, len(active_rooms))
            else:
                heapq.heappushpop(active_rooms, e)
        return max_rooms
```

- like in [[252-meeting-rooms]], we sort the [[intervals|intervals]] by starting time.
- then, we use a [[heap]] to keep track of the rooms that are currently in use.
	- we use a min-heap so that we know which room will become available first.
	- if the next meeting starts after this room becomes available, we can just use this room and update the end time on this room instead of using another new room.

[[sorting]], [[array]], [[priority-queue]]