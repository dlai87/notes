## Copy list with random pointer 

<https://www.lintcode.com/problem/copy-list-with-random-pointer/description>

没啥难度，先顺序copy，然后再copy random。 random在造列表时候用哈希表存下对应关系。



```python
class Solution:
    # @param head: A RandomListNode
    # @return: A RandomListNode
    def copyRandomList(self, head):
        dummy = RandomListNode(0)
        nodeMap = {}
        orig = head
        copy = dummy
        while orig: 
            temp = RandomListNode(orig.label)
            copy.next = temp
            copy = copy.next
            nodeMap[temp.label] = temp
            orig = orig.next

        orig = head
        copy = dummy
        while orig: 
            copy = copy.next
            if orig.random:
                copy.random = nodeMap[orig.random.label]
            orig = orig.next
        return dummy.next 
            
        
```

