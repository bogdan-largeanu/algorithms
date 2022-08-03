
# Problem
link: https://leetcode.com/problems/binary-tree-level-order-traversal/

```
Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

 

Example 1:


Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
Example 2:

Input: root = [1]
Output: [[1]]
Example 3:

Input: root = []
Output: []
 

Constraints:

The number of nodes in the tree is in the range [0, 2000].
-1000 <= Node.val <= 1000
```


# Solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        levels = {}
        if root == None:
            return []
#  we can recurse DFS over the entire tree. While so, for each call we keep track and increase our height. 
#  We will also use the height as an key in a hashmap, where we can save every element from that level.
        def parse(node,height):
            if node != None:
                if node.val != None:
#                     if we already have elements , we extend the array with current element being at the same height
                    if levels.get(height):
                        arr = levels.get(height)
                        arr.append(node.val)
                        levels[height] = arr
                        
                    else:
                        levels[height] = [node.val]
#                         we parse the rest of the tree until all nodes and heights have been parsed , at the end will have a hasmap with elements from every level
                parse(node.left,height +1)
                parse(node.right,height + 1)
        parse(root,0)
        result = []    
# We iterate over every key/tree level from hashmap and convert them into one array with other arr elements
        for key in levels:
            result.append(levels[key])
        return result
```