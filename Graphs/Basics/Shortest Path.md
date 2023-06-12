
# Problem
link: https://www.structy.net/problems/shortest-path
Write a function, shortest_path, that takes in a list of edges for an undirected graph and two nodes (node_A, node_B). The function should return the length of the shortest path between A and B. Consider the length as the number of edges in the path, not the number of nodes. If there is no path between A and B, then return -1.

edges = [
  ['w', 'x'],
  ['x', 'y'],
  ['z', 'y'],
  ['z', 'v'],
  ['w', 'v']
]

shortest_path(edges, 'w', 'z') # -> 2
edges = [
  ['w', 'x'],
  ['x', 'y'],
  ['z', 'y'],
  ['z', 'v'],
  ['w', 'v']
]

shortest_path(edges, 'y', 'x') # -> 1
edges = [
  ['a', 'c'],
  ['a', 'b'],
  ['c', 'b'],
  ['c', 'd'],
  ['b', 'd'],
  ['e', 'd'],
  ['g', 'f']
]

shortest_path(edges, 'a', 'e') # -> 3
edges = [
  ['a', 'c'],
  ['a', 'b'],
  ['c', 'b'],
  ['c', 'd'],
  ['b', 'd'],
  ['e', 'd'],
  ['g', 'f']
]

shortest_path(edges, 'e', 'c') # -> 2
edges = [
  ['a', 'c'],
  ['a', 'b'],
  ['c', 'b'],
  ['c', 'd'],
  ['b', 'd'],
  ['e', 'd'],
  ['g', 'f']
]

shortest_path(edges, 'b', 'g') # -> -1
edges = [
  ['c', 'n'],
  ['c', 'e'],
  ['c', 's'],
  ['c', 'w'],
  ['w', 'e'],
]

shortest_path(edges, 'w', 'e') # -> 1
edges = [
  ['c', 'n'],
  ['c', 'e'],
  ['c', 's'],
  ['c', 'w'],
  ['w', 'e'],
]

shortest_path(edges, 'n', 'e') # -> 2
edges = [
  ['m', 'n'],
  ['n', 'o'],
  ['o', 'p'],
  ['p', 'q'],
  ['t', 'o'],
  ['r', 'q'],
  ['r', 's']
]

shortest_path(edges, 'm', 's') # -> 6

# Solution

Summary: We want to use BFS because it allows for an easy counter +1 for each new level we traverse. We add this counter on the queue of tasks and return once we found the final node. We store all visited nodes in a set, to avoid cycles. (don't forget to always add the first starting node there)

```python

from collections import defaultdict, deque

def shortest_path(edges, node_A, node_B):
  graph = build_graph(edges)
#   we store visited points to avoid a cycle
  visited = set([node_A])
  
#   we store the node and distance so far
  queue = deque([(node_A,0)])
    
  
#   we do BFS and increase by 1
  while queue:
    node, distance = queue.popleft()
#     if we find the final mark we return the distance
    if node == node_B:
      return distance
    
    for neighbor in graph[node]:
      if neighbor not in visited:
        visited.add(neighbor)
        queue.append( (neighbor,distance+1))
      
  
  return -1
  
def build_graph(edges):
  graph = defaultdict(list)
  
  for a,b in edges:
    graph[a].append(b)
    graph[b].append(a)
  
  return graph
  
  
edges1 = [
  ['w', 'x'],
  ['x', 'y'],
  ['z', 'y'],
  ['z', 'v'],
  ['w', 'v']
] 


print(build_graph(edges1))
assert(shortest_path(edges1, 'w', 'z') == 2)
```