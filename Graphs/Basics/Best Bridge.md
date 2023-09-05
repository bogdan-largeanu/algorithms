# Problem best bridge
url: https://www.structy.net/problems/premium/best-bridge

Write a function, best_bridge, that takes in a grid as an argument. The grid contains water (W) and land (L). There are exactly two islands in the grid. An island is a vertically or horizontally connected region of land. Return the minimum length bridge needed to connect the two islands. A bridge does not need to form a straight line.

grid = [
  ["W", "W", "W", "L", "L"],
  ["L", "L", "W", "W", "L"],
  ["L", "L", "L", "W", "L"],
  ["W", "L", "W", "W", "W"],
  ["W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W"],
]
best_bridge(grid) # -> 1
grid = [
  ["W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W"],
  ["L", "L", "W", "W", "L"],
  ["W", "L", "W", "W", "L"],
  ["W", "W", "W", "L", "L"],
  ["W", "W", "W", "W", "W"],
]
best_bridge(grid) # -> 2
grid = [
  ["W", "W", "W", "W", "W"],
  ["W", "W", "W", "L", "W"],
  ["L", "W", "W", "W", "W"],
]
best_bridge(grid) # -> 3
grid = [
  ["W", "W", "W", "W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W", "L", "W", "W"],
  ["W", "W", "W", "W", "L", "L", "W", "W"],
  ["W", "W", "W", "W", "L", "L", "L", "W"],
  ["W", "W", "W", "W", "W", "L", "L", "L"],
  ["L", "W", "W", "W", "W", "L", "L", "L"],
  ["L", "L", "L", "W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W", "W", "W", "W"],
]
best_bridge(grid) # -> 3
grid = [
  ["L", "L", "L", "L", "L", "L", "L", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "W", "W", "L", "W", "W", "W", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "W", "W", "W", "W", "W", "W", "L"],
  ["L", "L", "L", "L", "L", "L", "L", "L"],
]
best_bridge(grid) # -> 2
grid = [
  ["W", "L", "W", "W", "W", "W", "W", "W"],
  ["W", "L", "W", "W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W", "W", "L", "W"],
  ["W", "W", "W", "W", "W", "W", "L", "L"],
  ["W", "W", "W", "W", "W", "W", "W", "L"],
]
best_bridge(grid) # -> 8


# Solution

Summary: 
1. We need to find the first island and mark all its positions as visited with distance 0
2. We add the first island to a BFS queue and start counting distance +1 
3. When we found the second island we return the distance as that will be the shortest distance. 

```python
from collections import deque 

def best_bridge(grid):
  visited = {}
  
# find first island 
  for r in range(len(grid)):
    for c in range(len(grid[0])):
      if grid[r][c] == "L":
        bfs(grid,r,c,visited)
        break
    if len(visited)>0:
      break
  

  queue = deque([])
# add first island to queue   
  for r,c in visited:
    queue.append((r,c,0))

#   BFS 
  while queue:
    r,c,distance = queue.popleft()
    
    left = r-1 , c 
    right = r+1 , c 
    up = r, c+1 
    down = r, c-1 


    for x,y in [left,right,up,down]:
      print("inside",x,y)
      if not positionIsValid(grid,x,y):
        continue
      #  if already in main island skip
      isVisited = (x,y) in visited 

      #  if is land and never visited, then is our bridge
      if  not isVisited and grid[x][y] == "L":
        return distance 
        
    #  if valid position and not visited already
      if positionIsValid(grid,x,y) and not isVisited:
        queue.append((x,y,distance+1))
        visited[x,y] = distance+1
    
    
        
def positionIsValid(grid,r,c):
  validHorizonatal = 0 <= r < len(grid)
  validVertical  = 0 <= c < len(grid[0])      
  return validVertical and validHorizonatal
  
  
def bfs(grid,r,c,distance):  
  queue = deque([])
  queue.append((r,c))
  
  while queue:
    r,c = queue.popleft()
    
    left = r-1 , c 
    right = r+1 , c 
    up = r, c+1 
    down = r, c-1 
    
    for x,y in [(r,c) ,left,right,up,down]:
      # print("xy",x,y,positionIsValid(grid,x,y),grid[x][y] == "L")
#      Save all land connected as distance 0
      if (x,y) not in distance and positionIsValid(grid,x,y) and grid[x][y] == "L":
        distance[(x,y)] = 0
        queue.append((x,y))

  return distance
      
      
      
      
grid = [
  ["W", "W", "W", "W", "W"],
  ["W", "W", "W", "W", "W"],
  ["L", "L", "W", "W", "L"],
  ["W", "L", "W", "W", "L"],
  ["W", "W", "W", "L", "L"],
  ["W", "W", "W", "W", "W"],
]
result = best_bridge(grid) # -> 2
print("result",result)
```