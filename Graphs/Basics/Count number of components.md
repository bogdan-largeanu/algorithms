
## Problem 
url: https://www.structy.net/problems/connected-components-count

Write a function, connected_components_count, that takes in the adjacency list of an undirected graph. The function should return the number of connected components within the graph.
```
test_00:
connected_components_count({
  0: [8, 1, 5],
  1: [0],
  5: [0, 8],
  8: [0, 5],
  2: [3, 4],
  3: [2, 4],
  4: [3, 2]
}) # -> 2
test_01:
connected_components_count({
  1: [2],
  2: [1,8],
  6: [7],
  9: [8],
  7: [6, 8],
  8: [9, 7, 2]
}) # -> 1
test_02:
connected_components_count({
  3: [],
  4: [6],
  6: [4, 5, 7, 8],
  8: [6],
  7: [6],
  5: [6],
  1: [2],
  2: [1]
}) # -> 3
test_03:
connected_components_count({}) # -> 0
test_04:
connected_components_count({
  0: [4,7],
  1: [],
  2: [],
  3: [6],
  4: [0],
  6: [3],
  7: [0],
  8: []
}) # -> 5
```

## Solution

Summary:
1. iterate over each key value in graph
2. check if is visited, if not increase count +1 and do DFS. mark every node visited
3. Continue until the list is finished


```python
def connected_components_count(graph):

  count = 0
  visited = set()
  
  def dfs(node,graph,visited):
    stack = [node]
    
    while len(stack) != 0:
      cur = stack.pop()
      if cur not in visited:
        stack.extend(graph[cur])
        visited.add(cur)
        
          
      
  for k in graph:
    if k not in visited:
      count +=1
      dfs(k,graph,visited)
        
  return count      
  

assert(connected_components_count({
  3: [],
  4: [6],
  6: [4, 5, 7, 8],
  8: [6],
  7: [6],
  5: [6],
  1: [2],
  2: [1]
}) == 3) # -> 3
```