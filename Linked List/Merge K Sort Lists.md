
## Problem
link: 

```md
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

 

Example 1:

Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
Example 2:

Input: lists = []
Output: []
Example 3:

Input: lists = [[]]
Output: []
 

Constraints:

k == lists.length
0 <= k <= 104
0 <= lists[i].length <= 500
-104 <= lists[i][j] <= 104
lists[i] is sorted in ascending order.
The sum of lists[i].length will not exceed 104.
```

## Solution

Summary. Merge list 2 at a time like in merge sort. Complexity O(K Log N)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        if not lists or len(lists) == 0:
            return None
        
#         iterave over each arr and 2 at a time , like in merge sort (This is a lot faster then merge 1 2 3 4 consecutive as the time complexity is K Log N instead of KN)
        
        while len(lists) >1:
            merge_lists = []
            for i in range(0,len(lists),2):
                l1 = lists[i]
                l2 = lists[i+1] if (i+1)< len(lists) else None
                merge_lists.append(self.merge(l1,l2))
        # with the new merge list , we loop over it until we only have one element
            lists = merge_lists
        return lists[0]

    #  Merge 2 order linked list.
    # create new node, and append the smaller value. 
    def merge(self,l1,l2):
        head = ListNode()
        tail = head
        
        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
        # When either list is finished we add the rest of element left in the other list
        if not l1:
            tail.next = l2
        if not l2:
            tail.next = l1
            
        return head.next
```