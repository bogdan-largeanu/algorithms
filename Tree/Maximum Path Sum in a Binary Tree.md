## Problem
link: https://leetcode.com/problems/binary-tree-maximum-path-sum/

```md
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.

 

Example 1:


Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
Example 2:


Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
 

Constraints:

The number of nodes in the tree is in the range [1, 3 * 104].
-1000 <= Node.val <= 1000
```

## Solution

We parse the tree and save the max values. 
We watch for 
- When tree splits right and left, we can only pick one path for sum, so we calculate with max the best one
- There is always the option of picking a branch or 0. Because a branch can be negative is better to not add it to the sum at all


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        #  use an array because a variable throws not initialise exception 
        result = [root.val]
        
        def dfs(node):
            if not node:
                return 0
            
#             parse the tree left and right
            left = dfs(node.left)
            right = dfs(node.right)
            
#           in each parsing there is always the change the values down are negative, so always want to grab the maximum between 0 and that branch. 0 means we don't use those values for the path
            leftMax = max(left,0)
            rightMax = max(right,0)
#             why ? node.val + leftMax + rightMax > because from left to node to right can be path. That won't work if you do node then split like below, there we have to choise either left or right
            result[0] = max(result[0], node.val + leftMax + rightMax)
            
#         return current val + max of left or right branch 
            return node.val + max(leftMax,rightMax)
        
        dfs(root)   
        
        return result[0]
```