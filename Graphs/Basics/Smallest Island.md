## Problem Minimum island

url: https://www.structy.net/problems/minimum-island



Write a function, minimum_island, that takes in a grid containing Ws and Ls. W represents water and L represents land. The function should return the size of the smallest island. An island is a vertically or horizontally connected region of land.

You may assume that the grid contains at least one island.

grid = [
  ['W', 'L', 'W', 'W', 'W'],
  ['W', 'L', 'W', 'W', 'W'],
  ['W', 'W', 'W', 'L', 'W'],
  ['W', 'W', 'L', 'L', 'W'],
  ['L', 'W', 'W', 'L', 'L'],
  ['L', 'L', 'W', 'W', 'W'],
]

minimum_island(grid) # -> 2


## Solution

Summary: Go over arr, perform a DFS recursive adding up the numbers with 1 for each level. Define base layers to return 0


```python

def minimum_island(grid):
  # parse each element in array 
#   explore DFS recursive
#  if it returns 0 ignore, if is > 0 calculate min(current_min, explore_function)
  min_size = float('inf')
  visited = set()
  for r in range(len(grid)):
    for c in range(len(grid[r])):
      print(r,c)
      result = explore(r,c,grid,visited)
      if result > 0 and result < min_size:
          min_size = result 
    
  return min_size
      
      
      
def explore(r,c,grid,visited):
  row_bounds = 0 <= r < len(grid)
  col_bounds = 0 <= c < len(grid[0])
  
  if not row_bounds or not col_bounds:
    return 0

  #   if is water stop 
  if grid[r][c] == "W":
    return 0
  
  pos = (r,c)
  if pos  in visited:
    return 0
  visited.add(pos)
  
  score = 1
  score += explore(r+1,c,grid,visited)
  score += explore(r-1,c,grid,visited)
  score += explore(r,c+1,grid,visited) 
  score += explore(r,c-1,grid,visited)
  return score
      
      
      
      
      
grid = [
  ['W', 'L', 'W', 'W', 'W'],
  ['W', 'L', 'W', 'W', 'W'],
  ['W', 'W', 'W', 'L', 'W'],
  ['W', 'W', 'L', 'L', 'W'],
  ['L', 'W', 'W', 'L', 'L'],
  ['L', 'L', 'W', 'W', 'W'],
]

minimum_island(grid) # -> 2


```

