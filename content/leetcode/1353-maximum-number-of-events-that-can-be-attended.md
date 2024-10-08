---
type: leetcode
title: 1353. maximum number of events that can be attended
tags:
  - heap
  - sorting
  - greedy
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-08-25
updated: 2024-08-25
---

You are given an array of `events` where `events[i] = [startDayi, endDayi]`. Every event `i` starts at `startDayi` and ends at `endDayi`.

You can attend an event `i` at any day `d` where `startTimei <= d <= endTimei`. You can only attend one event at any time `d`.

Return _the maximum number of events you can attend_.

## solution

The main intuition to keep in mind is:

Given any point in time $t$, if we could attend several events on date $t$, we should greedily attend the event that’s ending soonest, as that event will have the least flexibility/options to go in the future.

So, the solution is just the process of trying to figure out two problems:

1. At any time $t$, how do we know which events we can attend.
2. Given these events, how do we know which one ends first.

We can solve the first problem by sorting our events by start time, and then whenever we advance our time $t$, we just add the events that are now in the range to our active events.

For problem 2, use a min-heap on the end times of the events to always have the soonest ending event in constant time.

```python
def maxEvents(self, events: List[List[int]]) -> int:
	events.sort()
	# min-heap on (end, start)
	available_events = []
	event_ptr = 0
	  
	# t is set to the next free date for our dude
	t = events[0][0]
	ans = 0
	while event_ptr < len(events) or available_events:
		# add events that are now in range to heap
		while event_ptr < len(events) and events[event_ptr][0] <= t:
			heapq.heappush(
				available_events,
				(events[event_ptr][1], events[event_ptr][0])
			)
			event_ptr += 1

	if available_events:
		next_event = heapq.heappop(available_events)
		# event could already be over
		# only advance t and add to ans if still valid
		if next_event[0] >= t:
			t += 1
			ans += 1
		else:
			# advance t to next relevant date
			t = events[event_ptr][0]
	return ans
```
