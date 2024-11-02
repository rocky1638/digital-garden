---
type: leetcode
title: 1810. minimum path cost in a hidden grid
tags:
  - simulation
  - dfs
  - djikstra
aliases: 
parents: 
children: 
supports: 
enemies: 
date: 2024-10-27
updated: 2024-10-27
---

This is an **interactive problem**.

There is a robot in a hidden grid, and you are trying to get it from its starting cell to the target cell in this grid. The grid is of size `m x n`, and each cell in the grid is either empty or blocked. It is **guaranteed** that the starting cell and the target cell are different, and neither of them is blocked.

Each cell has a **cost** that you need to pay each time you **move** to the cell. The starting cell's cost is **not** applied before the robot moves.

You want to find the minimum total cost to move the robot to the target cell. However, you **do not know** the grid's dimensions, the starting cell, nor the target cell. You are only allowed to ask queries to the `GridMaster` object.

The `GridMaster` class has the following functions:

- `boolean canMove(char direction)` Returns `true` if the robot can move in that direction. Otherwise, it returns `false`.
- `int move(char direction)` Moves the robot in that direction and returns the cost of moving to that cell. If this move would move the robot to a blocked cell or off the grid, the move will be **ignored**, the robot will remain in the same position, and the function will return `-1`.
- `boolean isTarget()` Returns `true` if the robot is currently on the target cell. Otherwise, it returns `false`.

Note that `direction` in the above functions should be a character from `{'U','D','L','R'}`, representing the directions up, down, left, and right, respectively.

Return _the **minimum total cost** to get the robot from its initial starting cell to the target cell. If there is no valid path between the cells, return_ `-1`.

**Custom testing:**

The test input is read as a 2D matrix `grid` of size `m x n` and four integers `r1`, `c1`, `r2`, and `c2` where:

- `grid[i][j] == 0` indicates that the cell `(i, j)` is blocked.
- `grid[i][j] >= 1` indicates that the cell `(i, j)` is empty and `grid[i][j]` is the **cost** to move to that cell.
- `(r1, c1)` is the starting cell of the robot.
- `(r2, c2)` is the target cell of the robot.

Remember that you will **not** have this information in your code.

## solution

Because we don’t actually know what cells are available to us, we first DFS interactively using the robot, storing the costs and cells in a hashmap.

Then, we can run [[djikstras-algorithm]] to find the shortest path (we don’t even need the `master` for this step).

```python
def findShortestPath(self, master: 'GridMaster') -> int:
	visited = {(0,0): -1}
	dirs = [[-1,0],[0,1],[1,0],[0,-1]]
	target = None
	dir_strs = "URDL"
	reverse_dir_strs = "DLUR"
	  
	def dfs(x, y):
		nonlocal target
		if master.isTarget():
			target = (x, y)
			return True

		can_reach = False
		for i in range(4):
			dx, dy = dirs[i]
			ds = dir_strs[i]
			nx, ny = x+dx, y+dy
			if master.canMove(ds) and (nx, ny) not in visited:
				# move to (nx, ny) and dfs
				cost = master.move(ds)
				visited[(nx, ny)] = cost
				can_reach |= dfs(nx, ny)
				# move back
				master.move(reverse_dir_strs[i])
		return can_reach

	def djikstra(target):
		seen = set()
		seen.add((0, 0))
		# (cost, x, y)
		q = [(0,0,0)]
		while q:
			cost, x, y = heappop(q)
		  
			if (x, y) == target:
				return cost

			for dx, dy in dirs:
				nx, ny = x+dx, y+dy
				if (nx, ny) in visited:
					new_cost = cost + visited[(nx, ny)]
					if (nx, ny) not in seen:
						seen.add((nx, ny))
						heappush(q, (new_cost, nx, ny))
	  
	if not dfs(0, 0):
		return -1
	  
	return djikstra(target)
```
