---
type: leetcode
title: 489. robot room cleaner
tags:
  - backtracking
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-09-12
updated: 2024-09-12
---

You are controlling a robot that is located somewhere in a room. The room is modeled as an `m x n` binary grid where `0` represents a wall and `1` represents an empty slot.

The robot starts at an unknown location in the room that is guaranteed to be empty, and you do not have access to the grid, but you can move the robot using the given API `Robot`.

You are tasked to use the robot to clean the entire room (i.e., clean every empty cell in the room). The robot with the four given APIs can move forward, turn left, or turn right. Each turn is `90` degrees.

When the robot tries to move into a wall cell, its bumper sensor detects the obstacle, and it stays on the current cell.

## solution

We know that given a connected graph/path, DFS will fully explore it. The difficulty comes in trying to apply that to a black-box robot class, and needing to physically “backtrack” the robot, instead of just popping off of the recursive call stack.

So, knowing that the robot starts facing up, we start by trying to recurse upwards (setting starting point arbitrarily as `(0,0)`). Then, we will recurse on that next square until all directions are exhausted.

To backtrack, we physically turn the robot 180 degrees, move, and then rotate again to not change the initial direction of the robot.

```python
# """
# This is the robot's control interface.
# You should not implement it, or speculate about its implementation
# """
#class Robot:
# def move(self):
# """
# Returns true if the cell in front is open and robot moves into the cell.
# Returns false if the cell in front is blocked and robot stays in the current cell.
# :rtype bool
# """
#
# def turnLeft(self):
# """
# Robot will stay in the same cell after calling turnLeft/turnRight.
# Each turn will be 90 degrees.
# :rtype void
# """
#
# def turnRight(self):
# """
# Robot will stay in the same cell after calling turnLeft/turnRight.
# Each turn will be 90 degrees.
# :rtype void
# """
#
# def clean(self):
# """
# Clean the current cell.
# :rtype void
# """
  
def cleanRoom(self, robot):
	seen = set()
	# up, right, down, left
	dirs = [[-1,0],[0,1],[1,0],[0,-1]]
	def go_back():
		robot.turnRight()
		robot.turnRight()
		robot.move()
		robot.turnRight()
		robot.turnRight()
	  
	def backtrack(cell, d):
		seen.add(cell)
		robot.clean()
	  
		for i in range(4):
			new_d = (d+i)%4
			new_cell = (
				cell[0]+dirs[new_d][0],
				cell[1]+dirs[new_d][1]
			)
			if new_cell not in seen and robot.move():
				backtrack(new_cell, new_d)
				go_back()
			robot.turnRight()

	backtrack((0, 0), 0)
```
