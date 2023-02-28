## Problem
link: https://leetcode.com/problems/reverse-linked-list

```
Given the head of a singly linked list, reverse the list, and return the reversed list.

 

Example 1:

Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

Example 2:

Input: head = [1,2]
Output: [2,1]

Example 3:

Input: head = []
Output: []

 

Constraints:

    The number of nodes in the list is the range [0, 5000].
    -5000 <= Node.val <= 5000

 

Follow up: A linked list can be reversed either iteratively or recursively. Could you implement both?

```

## Solution

Summary:  Imagine a bridge , we flip it from right to left ( None   a ---> b ---->)  (None <---- a <---- b)  
We keep track of past pointer. We point current next to pass, (storing next first), then continue to next one

Iterative Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev, curr = None,head
    
        while curr:
#             save future one
            nextOne = curr.next
#             point currentn node to previous one
            curr.next = prev
            prev = curr
            curr = nextOne
            
        return prev
        
```

Complexity
    Space: O(N)
    Time: O(N)