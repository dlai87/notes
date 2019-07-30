## Global and Local Inversions

### **Description**

中文English

给定一个`[0, 1, ...N - 1]`的排列`A`，其中`N`是`A`的长度.

全局逆序数是指满足`0 <= i < j < N` 且 `A[i] > A[j]`的数量.

局部逆序数是指满足`0 <= i < N` 且 `A[i] > A[i+1]`的数量.

如果全局逆序数和局部逆序数相等，返回`true`，否则返回`false`.



这题更像是数学题，主要是观察数学规律。

看了别人的解析后，代码写起来不难。

```python
class Solution:
    """
    @param A: an array
    @return: is the number of global inversions is equal to the number of local inversions
    """
    def isIdealPermutation(self, A):
        # Write your code here
        for i in range(len(A)-2): 
            for j in range(i+2, len(A)): 
                if A[j] < A[i]: 
                    return False
        return True

```

