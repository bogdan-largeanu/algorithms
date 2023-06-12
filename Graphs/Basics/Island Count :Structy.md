# Problem Island count

link: https://www.structy.net/problems/island-count

Write a function, _island\_count_, that takes in a grid containing Ws and Ls. W represents water and L represents land. The function should return the number of islands on the grid. An island is a vertically or horizontally connected region of land.

```
grid = [
  ['W', 'L', 'W', 'W', 'W'],
  ['W', 'L', 'W', 'W', 'W'],
  ['W', 'W', 'W', 'L', 'W'],
  ['W', 'W', 'L', 'L', 'W'],
  ['L', 'W', 'W', 'L', 'L'],
  ['L', 'L', 'W', 'W', 'W'],
]

island_count(grid) # -> 3
```

```
grid = [
  ['L', 'W', 'W', 'L', 'W'],
  ['L', 'W', 'W', 'L', 'L'],
  ['W', 'L', 'W', 'L', 'W'],
  ['W', 'W', 'W', 'W', 'W'],
  ['W', 'W', 'L', 'L', 'L'],
]

island_count(grid) # -> 4
```

```
grid = [
  ['L', 'L', 'L'],
  ['L', 'L', 'L'],
  ['L', 'L', 'L'],
]

island_count(grid) # -> 1
```

```
grid = [
  ['W', 'W'],
  ['W', 'W'],
  ['W', 'W'],
]

island_count(grid) # -> 0
```

# Solution
Summary: 
- Iterate the 2d array
- when we find an island, check if is not visited already. 
  - If is not, counter=+1  and perform dfs or bfs (up down left right) marking all as visited
- return the counter at the end


```python
from collections import deque 


def island_count(grid):
  visited = set()
  counter = 0
  for r in range(0,len(grid)):
    for c in range(0,len(grid[r])):
      print("PARSE POS",r,c,grid[r][c])
      
      if grid[r][c] == "L" and (r,c) not in visited:
        counter +=1 
        visited = dfs(r,c,grid,visited)
  
  return counter
        
      
      

def dfs(r,c,grid,visited):
  queue = deque([(r,c)])
  visited.add((r,c))
  
  while queue:
    r, c = queue.popleft()
    print("DFS",r,c)

    #  we go in all directions
    left = (r,c-1)
    right = (r,c+1)
    up = (r-1,c)
    down = (r+1,c)
    
    for pos in [left,right,up,down]:
      if pos not in visited and isIsland(pos,grid,visited):
        queue.append(pos)
        visited.add(pos)
    
  return visited
    

def isIsland(pos,grid,visited):
  r,c = pos
  if r < 0 or r >= len(grid):
    return False
  if c < 0 or c >= len(grid[0]):
    return False
  
  if grid[r][c] == "L":
    return True
  
  return False

grid = [
  ['W', 'L', 'W', 'W', 'W'],
  ['W', 'L', 'W', 'W', 'W'],
  ['W', 'W', 'W', 'L', 'W'],
  ['W', 'W', 'L', 'L', 'W'],
  ['L', 'W', 'W', 'L', 'L'],
  ['L', 'L', 'W', 'W', 'W'],
]

print(island_count(grid), "should be 3")
# assert island_count(grid) == 3 # -> 3
```