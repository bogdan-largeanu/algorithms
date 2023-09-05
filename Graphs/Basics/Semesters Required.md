## Problem Semesters required
```

Write a function, semesters_required, that takes in a number of courses (n) and a list of prerequisites as arguments. Courses have ids ranging from 0 through n - 1. A single prerequisite of (A, B) means that course A must be taken before course B. Return the minimum number of semesters required to complete all n courses. There is no limit on how many courses you can take in a single semester, as long the prerequisites of a course are satisfied before taking it.

Note that given prerequisite (A, B), you cannot take course A and course B concurrently in the same semester. You must take A in some semester before B.

You can assume that it is possible to eventually complete all courses.

num_courses = 6
prereqs = [
  (1, 2),
  (2, 4),
  (3, 5),
  (0, 5),
]
semesters_required(num_courses, prereqs) # -> 3
num_courses = 7
prereqs = [
  (4, 3),
  (3, 2),
  (2, 1),
  (1, 0),
  (5, 2),
  (5, 6),
]
semesters_required(num_courses, prereqs) # -> 5
num_courses = 5
prereqs = [
  (1, 0),
  (3, 4),
  (1, 2),
  (3, 2),
]
semesters_required(num_courses, prereqs) # -> 2
num_courses = 12
prereqs = []
semesters_required(num_courses, prereqs) # -> 1
num_courses = 3
prereqs = [
  (0, 2),
  (0, 1),
  (1, 2),
]
semesters_required(num_courses, prereqs) # -> 3
num_courses = 6
prereqs = [
  (3, 4),
  (3, 0),
  (3, 1),
  (3, 2),
  (3, 5),
]
semesters_required(num_courses, prereqs) # -> 2
```



## Solution

Summary: Longest running consecutive classes also means the highest number of semesters.   
That means finding the longest path of travels is the number of semester we need

```python
from collections import defaultdict 
def semesters_required(num_courses, prereqs):
  # create a hmap with distance create
#   convert prereq to graph with hmap
#   mark all nodes with no depencies as 1 (class with no dependencies )
#  Start a dfs travers from the list, until we hit a node with a distance and return +1 for each depth level
# if a node/class has 2 children, pick the max one before adding +1 
  
  distance = {}
  nodes = defaultdict(list)
#   make nodes for every course 
  for i in range(num_courses):
    nodes[i] = []
#   connect the nodes based on dependencies
  for a,b in prereqs:
    if b not in nodes[a]:
      nodes[a].append(b)
#   mark distance one for each node with no dependencies
  for node_key in nodes:
    if len(nodes[node_key]) == 0:
      distance[node_key] = 1
#   go over every node/class and do DFS to calculate distance
  for node_key in nodes:
    traverse_graph(distance,nodes,node_key)
  
  print(nodes)
  print(distance)
  
#   go over nodes and return the highest one
  return max(distance.values())

def traverse_graph(distance,nodes,curr_node):
    if curr_node in distance:
      return distance[curr_node]
    
    max_distance = 0
    for child_node in nodes[curr_node]:
      attempt_distance = traverse_graph(distance,nodes,child_node)
      max_distance = max(attempt_distance,max_distance)

    distance[curr_node] = max_distance + 1 
    
    return distance[curr_node]
      
    
num_courses = 6
prereqs = [
  (1, 2),
  (2, 4),
  (3, 5),
  (0, 5),
]
print('result1',semesters_required(num_courses, prereqs)) # -> 3
```