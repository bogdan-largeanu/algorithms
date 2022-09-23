## Problem
link: https://leetcode.com/problems/serialize-and-deserialize-binary-tree/

```md
1.   Serialize and Deserialize Binary Tree
Hard

7747

286

Add to List

Share
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

 

Example 1:


Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
Example 2:

Input: root = []
Output: []
 

Constraints:

The number of nodes in the tree is in the range [0, 104].
-1000 <= Node.val <= 1000
```

## Solution 

Summary:
For Serializing :
 We preform pre order travels to the binary tree adding each element to a list. The end of nodes represent our baseCase to stop the recursion. We mark them with a specific value that can be deserialized later on to a null

 Deserialize:
 We unpack the string in an array and perform again pre order travels, this time increasing a counter +1 , creating a node for each value and adding None if we the specific value used above to mark end of a node.



```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        :type root: TreeNode
        :rtype: str
        """
        vals = []
        
        def preOrder(node):
#             this is our baseCase for recursion
            if not node:
                vals.append("N")
                return
            
            vals.append(str(node.val))
            
            preOrder(node.left)
            preOrder(node.right)
        
        preOrder(root)
        result = "-".join(vals)
        print(result)
        
        return "£".join(vals)
        
                
                
    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        values = data.split("£")
        result = []
        self.i = 0
        
        def dfs():
            if values[self.i]=="N":
                self.i +=1
                result.append(None)
                return
            
            node = TreeNode(int(values[self.i]))
            self.i += 1
            node.left = dfs()
            node.right = dfs()
            
            return node
        
        
        return dfs()
        

# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))

```