## lowest-common-ancestor-of-a-binary-tree

<https://www.lintcode.com/problem/lowest-common-ancestor-of-a-binary-tree/description>



第一直觉的写法，通过，但是效率不高。 

```python
class Solution:
    """
    @param: root: The root of the binary search tree.
    @param: A: A TreeNode in a Binary.
    @param: B: A TreeNode in a Binary.
    @return: Return the least common ancestor(LCA) of the two nodes.
    """
    def lowestCommonAncestor(self, root, A, B):
        if root.val == A.val or root.val == B.val: 
            return root 
        aInLeft = self.contains(root.left, A) 
        bInLeft = self.contains(root.left, B)
        
        if aInLeft != bInLeft: 
            return root 
        if aInLeft and bInLeft:
            return self.lowestCommonAncestor(root.left, A, B)
        else: 
            return self.lowestCommonAncestor(root.right, A, B)
            
        
    def contains(self, root, node): 
        if root is None:
            return False
        if root.val == node.val: 
            return True
        return self.contains(root.left, node) or self.contains(root.right, node)
        

```



看了下曾经leetcode 写的话

"我们分别在root的左右子树中搜索p和q。如果在左子树中搜索到了p或者q，就将其结点赋给left；
    如果在右子树中搜索到了p或者q，就将其结点赋给right。
    而如果没有搜索到，则返回NULL。这样如果left和right都不为NULL，则说明p和q必然位于不同的子树上，
    则root就是最低公共祖先；否则left和right中那个不为NULL的就是最低公共祖先"

于是有了下面的改进版本： 

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
    @param: root: The root of the binary search tree.
    @param: A: A TreeNode in a Binary.
    @param: B: A TreeNode in a Binary.
    @return: Return the least common ancestor(LCA) of the two nodes.
    """
    def lowestCommonAncestor(self, root, A, B):
        if not all([root, A, B]):
            return None 
        if root.val == A.val or root.val == B.val: 
            return root
            
        left = self.lowestCommonAncestor(root.left, A, B)
        right = self.lowestCommonAncestor(root.right, A, B)
        
        if all([left, right]):
            return root
        
        return left if left else right
       
```

