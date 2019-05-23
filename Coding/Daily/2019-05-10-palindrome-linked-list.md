## Palindrome Linked List

https://www.lintcode.com/problem/palindrome-linked-list/description

+ 快慢两支针
+ 用一个stack 存储慢指针遍历 
+ 如果是奇数长度，（即 fast == null）, stack 先弹一个为敬
+ 对比慢指针和stack里面的内容
+ 注意点：下面的代码用了array 来实现栈，但是python 也有自带栈的函数，熟悉一下。 效率更高一点。 

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
    @param head: A ListNode.
    @return: A boolean.
    """
    def isPalindrome(self, head):
        dummy = ListNode(0, next=head)
        slow = dummy
        fast = dummy
        stack = [] 
        while fast and fast.next : 
            fast = fast.next.next 
            slow = slow.next 
            stack.append(slow.val)
        
        if not fast : 
            stack = stack[:-1]       # 数组操作方式
            
        while len(stack) > 0 : 
            slow = slow.next
            if stack.pop() != slow.val:    # stack 操作方式
                return False

        return True
        
        
```

