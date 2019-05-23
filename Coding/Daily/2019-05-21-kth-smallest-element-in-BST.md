## Kth smallest element in BST

https://www.lintcode.com/problem/kth-smallest-element-in-a-bst/my-submissions



中序遍历bst 

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
    @param root: the given BST
    @param k: the given k
    @return: the kth smallest element in BST
    """
    def kthSmallest(self, root, k):
        self.count = 0 
        self.result = None 
        self.helper(root, k)
        return self.result
        
    def helper(self, node, k): 
        if not node: 
            return 
        self.helper(node.left, k)
        self.count += 1 
        if self.count == k:
            self.result = node.val
            return 
        self.helper(node.right, k)
```

