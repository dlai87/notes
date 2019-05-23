## Evaluate Reverse Polish Notation 

https://www.lintcode.com/problem/evaluate-reverse-polish-notation/description





```python
class Solution:
    """
    @param tokens: The Reverse Polish Notation
    @return: the value
    """
    def evalRPN(self, tokens):
        dict_op = { '+': (lambda x, y: x+y),
                    '-': (lambda x, y: x-y), 
                    '*': (lambda x, y: int(x*y)),
                    '/': (lambda x, y: int(x/y))
        }
        
        stack = [] 
        for token in tokens: 
            if token in dict_op: 
                num1 = stack.pop()
                num2 = stack.pop()
                stack.append(dict_op[token](num2, num1))
            else: 
                stack.append(int(token))
        return int(stack.pop())
```

