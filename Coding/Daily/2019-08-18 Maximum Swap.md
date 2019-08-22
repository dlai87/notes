## 1095. Maximum Swap

Given a non-negative integer. You could choose to swap two digits of it. Return the maximum valued number you could get.



```python
√class Solution:
    """
    @param num: a non-negative intege
    @return: the maximum valued number
    """
    def maximumSwap(self, num):
        # 数字转数组
        digits = [] 
        while num > 0:
            digits.append(num % 10)
            num //= 10 
        digits.reverse()  # 数组翻转。 注意不是sorted+reverse 

        # 寻找每个数字的最后index 
        index = {} 
        for i in range(len(digits)): 
            digit = digits[i]
            index[digit] = i 
        
        # 从前完后遍历digits     
        for i in range(len(digits)): 
            digit = digits[i]
            # 找有没有比当前大的数字，index 在其后面 
            for j in range(9, digit, -1): 
                if j in index and index[j] > i : 
                    temp = digits[i]
                    digits[i] = digits[index[j]]
                    digits[index[j]] = temp 
                    return self.arr_to_num(digits) 
        
        return self.arr_to_num(digits) 
            
    def arr_to_num(self, arr): 
        result = 0 
        t = 1 
        for i in range(len(arr)-1, -1, -1):
            result += arr[i] * t 
            t *= 10 
        return result
```