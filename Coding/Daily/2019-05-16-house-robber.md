## house robber 

https://www.lintcode.com/problem/house-robber/description 



dp 标准题

+ 没啥好说的，做不到3分钟一遍过都回去再练练

```python
class Solution:
    """
    @param A: An array of non-negative integers
    @return: The maximum amount of money you can rob tonight
    """
    def houseRobber(self, A):
        if not A : 
            return 0 
        if len(A) == 1 :
            return A[0]
        
        max_amount = [] 
        max_amount.append(A[0])
        max_amount.append(max(A[0],A[1]))
        for i in range(2, len(A)) : 
            value = max(A[i] + max_amount[i-2], max_amount[i-1])
            max_amount.append(value)
            
        return max_amount[-1]
            
        

```

