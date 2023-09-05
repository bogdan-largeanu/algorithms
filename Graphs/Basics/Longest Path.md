# Problem longest path

url: https://www.structy.net/problems/premium/longest-path

```

Write a function, longest_path, that takes in an adjacency list for a directed acyclic graph. The function should return the length of the longest path within the graph. A path may start and end at any two nodes. The length of a path is considered the number of edges in the path, not the number of nodes.

graph = {
  'a': ['c', 'b'],
  'b': ['c'],
  'c': []
}

longest_path(graph) # -> 2
graph = {
  'a': ['c', 'b'],
  'b': ['c'],
  'c': [],
  'q': ['r'],
  'r': ['s', 'u', 't'],
  's': ['t'],
  't': ['u'],
  'u': []
}

longest_path(graph) # -> 4
graph = {
  'h': ['i', 'j', 'k'],
  'g': ['h'],
  'i': [],
  'j': [],
  'k': [],
  'x': ['y'],
  'y': []
}

longest_path(graph) # -> 2
graph = {
  'a': ['b'],
  'b': ['c'],
  'c': [],
  'e': ['f'],
  'f': ['g'],
  'g': ['h'],
  'h': []
}

longest_path(graph) # -> 3

```

# Solution


Summary: Find ending nodes and go back on them counting the distance. 
Save the distance in a hmap and for all children/neighbors take the max distance

```Python

def longest_path(graph):
  distance = {}
  
  for key in graph:
    if len(graph[key]) == 0:
      distance[key] = 0
  
  
  for node in graph:
    traverse_graph(graph,distance,node)
  
  print(distance)
  return max(distance.values())
    
def traverse_graph(graph,distance,node):
  if node in distance:
    return distance[node]
  
  max_distance = 0

  for neighbour in graph[node]:
    attempt = traverse_graph(graph,distance,neighbour)
    distance[neighbour] = attempt
    max_distance = max(max_distance,attempt)
  
  distance[node] = max_distance +1 
  
  return distance[node]
    
  

  ```