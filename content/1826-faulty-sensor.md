---
type: leetcode
title: 1826. faulty sensor
tags:
  - two-pointer
  - array
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-11-01
updated: 2024-11-01
---

An experiment is being conducted in a lab. To ensure accuracy, there are **two** sensors collecting data simultaneously. You are given two arrays `sensor1` and `sensor2`, where `sensor1[i]` and `sensor2[i]` are the `ith` data points collected by the two sensors.

However, this type of sensor has a chance of being defective, which causes **exactly one** data point to be dropped. After the data is dropped, all the data points to the **right** of the dropped data are **shifted** one place to the left, and the last data point is replaced with some **random value**. It is guaranteed that this random value will **not** be equal to the dropped value.

- For example, if the correct data is `[1,2,**3**,4,5]` and `3` is dropped, the sensor could return `[1,2,4,5,**7**]` (the last position can be **any** value, not just `7`).

We know that there is a defect in **at most one** of the sensors. Return _the sensor number (_`1` _or_ `2`_) with the defect. If there is **no defect** in either sensor or if it is **impossible** to determine the defective sensor, return_ `-1`_._

## solution

Two pointers, but just a lot of edge cases.

```python
def badSensor(self, sensor1: List[int], sensor2: List[int]) -> int:
	n = len(sensor1)
	if n < 2:
		return -1
	  
	p1 = p2 = 0
	while p1 < n and p2 < n:
		if sensor1[p1] == sensor2[p2]:
			p1 += 1
			p2 += 1
		else:
			# if we've reached last two values, we can't determine anything
			if p1+1 == n:
				return -1
			# can't determine yet
			if sensor1[p1+1] == sensor2[p2] and sensor1[p1] == sensor2[p2+1]:
				p1 += 1
				p2 += 1
			# needed to slide p1 up to match, so 2 was faulty
			elif sensor1[p1+1] == sensor2[p2]:
				return 2
			elif sensor1[p1] == sensor2[p2+1]:
				return 1
	return -1
```
