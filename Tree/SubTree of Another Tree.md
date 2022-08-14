
## Problem
```python
Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

 

Example 1:

Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true

Example 2:

Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false

 

Constraints:

    The number of nodes in the root tree is in the range [1, 2000].
    The number of nodes in the subRoot tree is in the range [1, 1000].
    -104 <= root.val <= 104
    -104 <= subRoot.val <= 104
```



## Solution

We split the problem in 2 parts. One is validating two trees are the same, the other one is parsing the tree.

```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not subRoot:
            return True
        if not root: #if there is not root but a subRoot exist then there is no Subtree
            return False
        # clean code. we don't need to double check root.val and subroot.val since this validates True or False already
        if self.validate(root,subRoot):
            return True
        # We can call and validate everytime because the OR will take care of returning True if a True value comes up along the way
        return self.isSubtree(root.left,subRoot) or self.isSubtree(root.right,subRoot)
            
    def validate(self,n1,n2):
        # if both have reach the end of the nodes, that means they are the same.
            if not n1 and not n2:
                return True
        # we call recursively if nodes match until both nodes are none, if not we return False
            if n1 and n2 and n1.val == n2.val:
                return self.validate(n1.left,n2.left) and self.validate(n1.right,n2.right)
            
            return False
```