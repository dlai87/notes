## Flatten Nested List Iterator 

https://www.lintcode.com/problem/flatten-nested-list-iterator/description



```python
"""
This is the interface that allows for creating nested lists.
You should not implement it, or speculate about its implementation

class NestedInteger(object):
    def isInteger(self):
        # @return {boolean} True if this NestedInteger holds a single integer,
        # rather than a nested list.

    def getInteger(self):
        # @return {int} the single integer that this NestedInteger holds,
        # if it holds a single integer
        # Return None if this NestedInteger holds a nested list

    def getList(self):
        # @return {NestedInteger[]} the nested list that this NestedInteger holds,
        # if it holds a nested list
        # Return None if this NestedInteger holds a single integer
"""

class NestedIterator(object):

    def __init__(self, nestedList):
        """
        Initialize your data structure here.
        :type nestedList: List[NestedInteger]
        """
        self.stack = [] 
        for element in nestedList[::-1]: 
            self.stack.append(element)
        print(len(self.stack))

    def next(self):
        """
        :rtype: int
        """
        return self.stack.pop().getInteger() 
        

    def hasNext(self):
        """
        :rtype: bool
        """
        while len(self.stack) > 0: 
            current = self.stack[-1]
            if current.getInteger() is not None: 
                return True
            else: 
                current = self.stack.pop()
                nList = current.getList()
                for element in nList[::-1]: 
                    self.stack.append(element)
        return False

```

