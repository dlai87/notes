## reorder list 

<https://www.lintcode.com/problem/reorder-list/description>



这题题意倒是不难，思路也很清晰，主要就是对于链表的操作。 

反转，插入等操作的理顺。 

没用纸笔做草稿，坑比较多，需要多测一些情况debug

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
    @param head: The head of linked list.
    @return: nothing
    """
    def reorderList(self, head):
        if not head:
            return head
        dummy = ListNode(0, next=head)
        slow = dummy
        fast = dummy
        while fast and fast.next: 
            fast = fast.next.next
            slow = slow.next
        head2 = self.reverseList(slow.next)
        slow.next = None
        return self.mergeTwoLists(head, head2)
    
    def reverseList(self, head): 
        if not head:
            return head
        dummy = ListNode(0, next=head)
        pre = dummy.next
        cur = pre.next
        pre.next = None
        while cur: 
            temp = cur.next 
            cur.next = pre 
            pre = cur
            cur = temp
        return pre
        
    def mergeTwoLists(self, head1, head2): 
        #self.printList(head1)
        #self.printList(head2)
        dummy = ListNode(0)
        cur = dummy
        ptr1 = head1
        ptr2 = head2
        flag = True
        while ptr1 and ptr2: 
            if flag: 
                cur.next = ptr1
                ptr1 = ptr1.next 
            else: 
                cur.next = ptr2
                ptr2 = ptr2.next
            cur = cur.next
            flag = not flag
        if ptr1: 
            cur.next = ptr1
            cur = cur.next
        if ptr2: 
            cur.next = ptr2
            cur = cur.next
        return dummy.next
        
    def printList(self, head):
        while head: 
            print(head.val)
            head = head.next
        print("====END===")
            

```

