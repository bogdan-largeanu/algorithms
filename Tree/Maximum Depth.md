
# Problem

leetcode: https://leetcode.com/problems/maximum-depth-of-binary-tree/
```
Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.



Example 1:


Input: root = [3,9,20,null,null,15,7]
Output: 3
Example 2:

Input: root = [1,null,2]
Output: 2
 

Constraints:

The number of nodes in the tree is in the range [0, 104].
-100 <= Node.val <= 100
```


# Solution 1 Recursive 

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
#         Recurse untill we hit base case and return 0
        if root == None:
            return 0
        else:
            left = self.maxDepth(root.left)
            
            right = self.maxDepth(root.right)
#             We recurse and add 1 for each level. We only return the maximum branch for each recursion
            return max(left,right) + 1

```

# Solution 2 Iteration 

```python

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root == None:
            return 0
        stack = []
#         we build a BFS , add level and node pointer on each
        stack.append((0,root))

        maxDepth = 0
        while stack != []:
#  We iterate over our stack of nodes, pop them off, and add is children back into the stack with a +1 for depth. 
# We stop only after vising all children
            depth,node = stack.pop()
            maxDepth = max(depth,maxDepth)
            if node != None:
                stack.append((depth+1,node.left))
                stack.append((depth+1,node.right))
        
        return maxDepth
```