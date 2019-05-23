## Roman to Integer 

https://www.lintcode.com/problem/roman-to-integer/description



主要是考察stack

```python
class Solution:
    """
    @param s: Roman representation
    @return: an integer
    """
                
    def romanToInt(self, s):
        dict = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500, 'M':1000}
        stack = [] 
        for c in s : 
            currentInt = dict[c]
            if len(stack) == 0 or stack[-1] >= currentInt: 
                stack.append(currentInt)
            else: 
                stack.append(currentInt - stack.pop())
                
                
        result = 0 
        while len(stack) > 0 : 
            result += stack.pop()
            
        return result
```

