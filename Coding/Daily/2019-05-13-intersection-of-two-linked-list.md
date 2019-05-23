## Intersection of Two Linked Lists

https://www.lintcode.com/problem/intersection-of-two-linked-lists/d

```python
"""
Definition of ListNode
class ListNode(object):
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    """
    @param headA: the first list
    @param headB: the second list
    @return: a ListNode
    """
    def getIntersectionNode(self, headA, headB):
        if not headA or not headB:
            return None 
        len_A = 0 
        len_B = 0 
        dummy_A = ListNode(0, headA)
        dummy_B = ListNode(0, headB)
        ptr_A, ptr_B = dummy_A, dummy_B
        while ptr_A: 
            ptr_A = ptr_A.next
            len_A += 1 
        while ptr_B:
            ptr_B = ptr_B.next
            len_B += 1 
        
        if len_A > len_B: 
            ptr_short, ptr_long = dummy_B.next, dummy_A.next
        else: 
            ptr_short, ptr_long = dummy_A.next, dummy_B.next
        
        for i in range(abs(len_A - len_B)): 
            ptr_long = ptr_long.next
        
        while ptr_short and ptr_long: 
            if ptr_short.val == ptr_long.val:
                return ptr_short
            ptr_short = ptr_short.next 
            ptr_long = ptr_long.next 
            
        return None 
```

