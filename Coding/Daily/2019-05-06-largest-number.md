## Largest number

https://www.lintcode.com/problem/largest-number/description

这题知识点：

+ python3 自定义sorted规则 
+ lambda 函数

```python
from functools import cmp_to_key

def customized_cmp(a, b): 
    if a + b < b + a : 
        return 1 
    return -1 
            
class Solution:
    """
    @param nums: A list of non negative integers
    @return: A string
    """
    def largestNumber(self, nums):
        # 全部int转str
        nums = [str(i) for i in nums]
        # 自定义排序规则
        nums = sorted(nums, key=cmp_to_key(customized_cmp))
				# str array join
        result = ''.join(nums)
        if len(result) > 1: 
            i = 0 
            while i < len(result):
                if result[i] != '0':
                    break
                i += 1 
            result = result[i:]
            if len(result) == 0:
                return '0'
        
        return result
```

