## Problem

link: 

```
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

 

Example 1:

Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

Example 2:

Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

Example 3:

Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.

 

Constraints:

    The number of the nodes in the list is in the range [0, 104].
    -105 <= Node.val <= 105
    pos is -1 or a valid index in the linked-list.

 

Follow up: Can you solve it using O(1) (i.e. constant) memory?
```


## Solution 
### Solution 1 with a hashmap Space Complexity O(N) Time Complexity O(N)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    
    def hmapSolution(self,head):
        hmap = {}
        
        curr = head
        while curr:
            if hmap.get(curr.val):
                if curr in hmap.get(curr.val):
                    return True
                else:
                    hmap[curr.val].append(curr)
            else:
                hmap[curr.val] = [curr]
            curr = curr.next
            
        return False
    
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        return self.hmapSolution(head)
        
```
### Solution 2 tortoise and hare 


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    
    def hareTortoiseSolution(self,head):
        hare,tortoise = head, head
#         We will have a fast and slow pointer. Fast pointer goes 2 nodes at a time
#       Think of the while loop as a recursive function that requires a good base case

        while hare and hare.next:
            hare = hare.next.next
            tortoise = tortoise.next
#             we move the pointers before checking the nodes to avoid situations where node is 1 element. [1]
            if hare == tortoise:
                return True
        return False
        
    
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        return self.hareTortoiseSolution(head)
        

```