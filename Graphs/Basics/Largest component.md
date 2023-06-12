## Problem

url: https://www.structy.net/problems/largest-component

Write a function, largest_component, that takes in the adjacency list of an undirected graph. The function should return the size of the largest connected component in the graph.
```
test_00:
largest_component({
  0: [8, 1, 5],
  1: [0],
  5: [0, 8],
  8: [0, 5],
  2: [3, 4],
  3: [2, 4],
  4: [3, 2]
}) # -> 4
test_01:
largest_component({
  1: [2],
  2: [1,8],
  6: [7],
  9: [8],
  7: [6, 8],
  8: [9, 7, 2]
}) # -> 6
test_02:
largest_component({
  3: [],
  4: [6],
  6: [4, 5, 7, 8],
  8: [6],
  7: [6],
  5: [6],
  1: [2],
  2: [1]
}) # -> 5
test_03:
largest_component({}) # -> 0
test_04:
largest_component({
  0: [4,7],
  1: [],
  2: [],
  3: [6],
  4: [0],
  6: [3],
  7: [0],
  8: []
}) # -> 3
```

## Solution

Summary: We go over each key and trigger a DFS. we count every element added in DFS queue.
We update the values with highest value for each DFS 


```python
def largest_component(graph):
  largestCount = 0
  visited = set()
  
  def dfs(node,graph,visited):
    stack = [node]
    count = 0
    while len(stack) != 0:
      cur = stack.pop()
      if cur not in visited:
        stack.extend(graph[cur])
        visited.add(cur)
        count +=1 
        
    return count
      
  for k in graph:
    if k not in visited:
      largestCount = max(largestCount,dfs(k,graph,visited))
  
  print(largestCount)
  return largestCount      


assert(largest_component({
  0: [8, 1, 5],
  1: [0],
  5: [0, 8],
  8: [0, 5],
  2: [3, 4],
  3: [2, 4],
  4: [3, 2]
}) ==4)

```