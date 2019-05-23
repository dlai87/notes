## Spiral Matrix 

https://www.lintcode.com/problem/spiral-matrix/description

这题就是看下标的使用。

+ 以下这种方式个人感觉比较清爽

```python 
class Solution:
    """
    @param matrix: a matrix of m x n elements
    @return: an integer list
    """
    def spiralOrder(self, matrix):
        result = [] 
        if not matrix: 
            return result
        up = 0
        down = len(matrix)-1
        right = len(matrix[0])-1
        left = 0 
        while True:
            for j in range(left, right+1): 
                result.append(matrix[up][j])
            up += 1 
            if up > down:  
                break
            for i in range(up, down+1):
                result.append(matrix[i][right])
            right -= 1 
            if left > right: 
                break
            for j in range(right, left-1, -1): 
                result.append(matrix[down][j])
            down -= 1 
            if up > down:
                break
            for i in range(down, up-1, -1): 
                result.append(matrix[i][left])
            left += 1 
            if left > right:
                break
        return result
        

```

