## Rotate list

https://www.lintcode.com/problem/rotate-list/description

链表题最好还是画一下图，不管多简单。

````python
"""
Definition of ListNode
class ListNode(object):
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    """
    @param head: the List
    @param k: rotate to the right k places
    @return: the list after rotation
    """
    def rotateRight(self, head, k):
        if not head:
            return head

        count = 0 
        temp = head
        while temp: 
            temp = temp.next
            count += 1 
        k = k % count
        
        if not k: 
            return head
        dummy = ListNode(0, next=head)
        fast = dummy.next
        slow = dummy.next
        for i in range(k):
            fast = fast.next 
            
        while fast.next:
            fast = fast.next
            slow = slow.next 

        dummy.next = slow.next
        slow.next = None
        fast.next = head
        return dummy.next
````

