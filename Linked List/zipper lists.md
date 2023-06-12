# Problem

Link: https://www.structy.net/problems/zipper-lists

```md
Write a function, zipper_lists, that takes in the head of two linked lists as arguments. The function should zipper the two lists together into single linked list by alternating nodes. If one of the linked lists is longer than the other, the resulting list should terminate with the remaining nodes. The function should return the head of the zippered linked list.

Do this in-place, by mutating the original Nodes.

You may assume that both input lists are non-empty.

test_00:
a = Node("a")
b = Node("b")
c = Node("c")
a.next = b
b.next = c
# a -> b -> c

x = Node("x")
y = Node("y")
z = Node("z")
x.next = y
y.next = z
# x -> y -> z

zipper_lists(a, x)
# a -> x -> b -> y -> c -> z
```


# Solution
Summary: Use a counter and check if even or not to iterate and point list1 or list2


```python
class Node:
  def __init__(self, val):
    self.val = val
    self.next = None

def zipper_lists(head_1, head_2):
  tail = head_1
  start = tail
  head_1 = head_1.next 
  
  count = 1
# on even we add head 1 or uneven we had head2
  while head_1 and head_2:
    if count % 2 == 0:
      tail.next = head_1
      head_1 = head_1.next  
    else:
      tail.next = head_2
      head_2 = head_2.next
    
    count +=1
    tail = tail.next
  
  if head_1:
    tail.next = head_1
    
  if head_2:
    tail.next = head_2

  
  return start
  

a = Node("a")
b = Node("b")
c = Node("c")
d = Node("d")
e = Node("e")
f = Node("f")
a.next = b
b.next = c
c.next = d
d.next = e
e.next = f
# a -> b -> c -> d -> e -> f

x = Node("x")
y = Node("y")
z = Node("z")
x.next = y
y.next = z
# x -> y -> z

result = zipper_lists(a,x)

print("test")
while result:
  print(result.val)
  result = result.next

```