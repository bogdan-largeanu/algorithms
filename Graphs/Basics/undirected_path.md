# Problem : Undirected path

```
Write a function, undirected_path, that takes in a list of edges for an undirected graph and two nodes (node_A, node_B). The function should return a boolean indicating whether or not there exists a path between node_A and node_B.

test_00:
edges = [
  ('i', 'j'),
  ('k', 'i'),
  ('m', 'k'),
  ('k', 'l'),
  ('o', 'n')
]

undirected_path(edges, 'j', 'm') # -> True
test_01:
edges = [
  ('i', 'j'),
  ('k', 'i'),
  ('m', 'k'),
  ('k', 'l'),
  ('o', 'n')
]

undirected_path(edges, 'm', 'j') # -> True
test_02:
edges = [
  ('i', 'j'),
  ('k', 'i'),
  ('m', 'k'),
  ('k', 'l'),
  ('o', 'n')
]

undirected_path(edges, 'l', 'j') # -> True
test_03:
edges = [
  ('i', 'j'),
  ('k', 'i'),
  ('m', 'k'),
  ('k', 'l'),
  ('o', 'n')
]

undirected_path(edges, 'k', 'o') # -> False
test_04:
edges = [
  ('i', 'j'),
  ('k', 'i'),
  ('m', 'k'),
  ('k', 'l'),
  ('o', 'n')
]

undirected_path(edges, 'i', 'o') # -> False
test_05:
edges = [
  ('b', 'a'),
  ('c', 'a'),
  ('b', 'c'),
  ('q', 'r'),
  ('q', 's'),
  ('q', 'u'),
  ('q', 't'),
]


undirected_path(edges, 'a', 'b') # -> True
test_06:
edges = [
  ('b', 'a'),
  ('c', 'a'),
  ('b', 'c'),
  ('q', 'r'),
  ('q', 's'),
  ('q', 'u'),
  ('q', 't'),
]

undirected_path(edges, 'a', 'c') # -> True
test_07:
edges = [
  ('b', 'a'),
  ('c', 'a'),
  ('b', 'c'),
  ('q', 'r'),
  ('q', 's'),
  ('q', 'u'),
  ('q', 't'),
]

undirected_path(edges, 'r', 't') # -> True
test_08:
edges = [
  ('b', 'a'),
  ('c', 'a'),
  ('b', 'c'),
  ('q', 'r'),
  ('q', 's'),
  ('q', 'u'),
  ('q', 't'),
]

undirected_path(edges, 'r', 'b') # -> False
test_09:
edges = [
  ('s', 'r'),
  ('t', 'q'),
  ('q', 'r'),
]

undirected_path(edges, 'r', 't') # -> True
```


## Solution

Summary: 
  1. convert the graph to a hmap
  2. Save visited notes to avoid infinite loops since nodes are undirected.
  3. parse the graph until you find the target or finish searching 

```python
from collections import deque,defaultdict

def undirected_path(edges, node_A, node_B):
  
  #   convert to a hmap the graph
  hmap = convertToDic(edges)
  
  
  q = deque()
  q.append(node_A)
  visited = set()
  # parse the graph until you find the target or finish searching 
  while len(q) != 0:
    current = q.pop()
    #  checked if node has been visited already
    if current in visited:
      continue
    
    children = hmap[current]

    if node_B == hmap[current] or node_B in children:
      return True
    #  mark as visited and add the notes to parse next
    visited.add(current)
    q.extend(children)
  
  return False
  
def convertToDic(edges):
  hmap = defaultdict(list)
  
  for l,r in edges:
    hmap[l].append(r)
    hmap[r].append(l)
    
  return hmap
  
  
  

edges = [
  ('i', 'j'),
  ('k', 'i'),
  ('m', 'k'),
  ('k', 'l'),
  ('o', 'n')
]
hmap = {'i': ['j', 'k'], 'j': ['i'], 'k': ['i', 'm', 'l'], 'm': ['k'], 'l': ['k'], 'o': ['n'], 'n': ['o']}

assert convertToDic(edges) == hmap
assert undirected_path(edges, 'j', 'm') == True
print(undirected_path(edges, 'j', 'm') )# -> True


```
