## Binary Tree Path Sum

https://www.lintcode.com/problem/binary-tree-path-sum/description

思路本质上是DFS. 注意点是， 往下一个node传递时候，需要复制原来的path并往下传。不能直接传原来的path。否则path会被改的面目全非。 



```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""


class Solution:
    """
    @param: root: the root of binary tree
    @param: target: An integer
    @return: all valid paths
    """
    def binaryTreePathSum(self, root, target):
        self.result = [] 
        if root: 
            path_nodes = [] 
            
            self.singlePath(root, list(path_nodes), target)  # 新建一个list，复制了原来的node 
        return self.result
        
    def singlePath(self, node, path_nodes, target): 
        path_nodes.append(node.val)
        if not node.left and not node.right:
            path_sum = 0 
            for n in path_nodes:
                path_sum += n 
            if path_sum == target: 
                self.result.append(path_nodes)

        if node.left:
            self.singlePath(node.left, list(path_nodes), target) #新建一个list，复制了原来的node 

        if node.right:
            self.singlePath(node.right, list(path_nodes), target) #新建一个list，复制原来nodes
```

