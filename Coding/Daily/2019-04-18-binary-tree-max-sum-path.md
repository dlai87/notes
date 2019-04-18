## Binary Tree Max Path Sum

<https://www.lintcode.com/problem/binary-tree-maximum-path-sum/description>

这题不需要把 single path 传递下去。因为不需要找出具体的path。 

如果有需要找到具体path 是什么， 才需要传递path

```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

import sys

class Solution:
    """
    @param root: The root of binary tree.
    @return: An integer
    """
    def maxPathSum(self, root):
        self.max_val = -sys.maxsize -1
        self.pathSum(root)
        return self.max_val
        
    def pathSum(self, node): 
        if node is None: 
            return 0 
        left_val = self.pathSum(node.left)
        right_val = self.pathSum(node.right)
        addValue = max(left_val+right_val, left_val, right_val, 0)
        if node.val + addValue > self.max_val: 
            self.max_val = node.val + addValue
        # 这里是精华所在，返回值只能是 left+root， right+root，或者 root
        # 不能够同时 left + right + root 
        # 否则不能和其他的点构成path 
        return_val = max(left_val, right_val, 0)
        # 返回值 node 节点必包括，所以node.val + return_val
        return node.val + return_val

```

