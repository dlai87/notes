## Print Binary Tree

https://www.lintcode.com/problem/print-binary-tree/description

+ 递归方式获得树高度
+ 层级遍历
+ 遍历放的index方式。tuple [start_index, end_index ] 

```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""
from collections import deque 

class Solution:
    """
    @param root: the given tree
    @return: the binary tree in an m*n 2D string array
    """
    def printTree(self, root):
        # Write your code here
        depth = self.getDepth(root)
        level_size =  (pow(2, depth)-1)
        indexQueue = deque()
        nodeQueue = deque()
        indexQueue.append([0, level_size-1])
        nodeQueue.append(root)
        result = [] 
        while len(nodeQueue) > 0 : 
            level_nodes = len(nodeQueue)
            level_output = [""] * (pow(2, depth)-1)
            for i in range(level_nodes): 
                node = nodeQueue.popleft()
                index = indexQueue.popleft()
                mid = (index[0] + index[1])//2 
                level_output[mid] = str(node.val)
                if node.left:
                    nodeQueue.append(node.left)
                    indexQueue.append([index[0],mid])
                if node.right:
                    nodeQueue.append(node.right)
                    indexQueue.append([mid+1, index[1]])
            result.append(level_output)
        return result
        
        
    def getDepth(self, root):
        if root == None:
            return 0 
        return max(self.getDepth(root.left), self.getDepth(root.right)) + 1 
```

