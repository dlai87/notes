## Maximum Width of Binary Tree



https://www.lintcode.com/problem/maximum-width-of-binary-tree/description



+ 层级遍历 binary tree
+ node index 的关系：  root index = N , left index = 2N+1 , right index = 2N +2 







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
    @param root: the root
    @return: the maximum width of the given tree
    """
    def widthOfBinaryTree(self, root):
        if not root :
            return 0 
        nodeQueue = deque()
        indexQueue = deque() 
        nodeQueue.append(root)
        indexQueue.append(0)
        max_width = 0 
        while len(nodeQueue) > 0 : 
            level = len(nodeQueue)
            left_index = 0 
            right_index = 0 
            for i in range(level): 
                node = nodeQueue.popleft()
                index = indexQueue.popleft()
                if left_index == 0:
                    left_index = index 
                else:
                    right_index = index 
                if (right_index-left_index+1) > max_width:
                    max_width = (right_index-left_index+1) 
                if node.left: 
                    nodeQueue.append(node.left)
                    indexQueue.append(index*2+1)
                if node.right:
                    nodeQueue.append(node.right)
                    indexQueue.append(index*2+2)
        return max_width
```

