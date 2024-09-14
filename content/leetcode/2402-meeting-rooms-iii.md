---
type: leetcode
title: 2402. meeting rooms iii
tags:
  - heap
  - sorting
  - hashmap
aliases: 
parents:
  - "[[252-meeting-rooms]]"
children: 
supports: 
enemies: 
date: 2024-05-19
updated: 2024-05-19
---

You are given an integer `n`. There are `n` rooms numbered from `0` to `n - 1`.

You are given a 2D integer array `meetings` where `meetings[i] = [starti, endi]` means that a meeting will be held during the **half-closed** time interval `[starti, endi)`. All the values of `starti` are **unique**.

Meetings are allocated to rooms in the following manner:

1. Each meeting will take place in the unused room with the **lowest** number.
2. If there are no available rooms, the meeting will be delayed until a room becomes free. The delayed meeting should have the **same** duration as the original meeting.
3. When a room becomes unused, meetings that have an earlier original **start** time should be given the room.

Return _the **number** of the room that held the most meetings._ If there are multiple rooms, return _the room with the **lowest** number._

A **half-closed interval** `[a, b)` is the interval between `a` and `b` **including** `a` and **not including** `b`.

## solution

The intuition here is quite similar to it’s predecessor, [[253-meetings-rooms-ii]], but also very similar to [[621-task-scheduler]]. We use min-heaps to keep track of both available rooms and in-progress meetings.

Finally, we use a timestamp `t` to keep track of the current time, and use the timestamp to “fast-forward” in time whenever we would need to wait (next meeting starts in the future, or no rooms available).

```python
def mostBooked(self, n: int, meetings: List[List[int]]) -> int:
	# min-heap, lowest numbered room at top
	avail_rooms = [i for i in range(n)]
	# min-heap, soonest ending meeting on top (end_time, room)
	in_progress = []
	count = Counter()
	  
	heapify(avail_rooms)
	  
	# sort meetings by start time
	meetings.sort(key=lambda x: x[0])
	meeting_idx = 0
	t = 0
	  
	while meeting_idx < len(meetings):
		# free up any finished meetings
		while len(in_progress) and in_progress[0][0] <= t:
			_, room = heappop(in_progress)
			heappush(avail_rooms, room)
		  
		next_meeting = meetings[meeting_idx]
		  
		# skip till next meeting needs to be scheduled
		if next_meeting[0] > t:
			t = next_meeting[0]

		# next meeting should start
		else:
			if len(avail_rooms):
				start_time = t
				end_time = t + (next_meeting[1] - next_meeting[0])
				room = heappop(avail_rooms)
				heappush(in_progress, (end_time, room))
				count[room] += 1
				meeting_idx += 1

			# no rooms avail, fast-forward until room is free
			else:
				t = in_progress[0][0]

	return max(count, key=count.get)
```
