## Rotate Image

https://www.lintcode.com/problem/rotate-image/description



思路，分析可得， 90度旋转， 对应公式是 

```    [i][j]  = [j][N-i]```

    1| 一轮swap相当于同时操作四个点才行。 
    2| 操作过的点避免重复操作, 从外围向中间操作。 每一轮操作相当于matrix少掉一圈边缘。

```python
class Solution:
    """
    @param matrix: a lists of integers
    @return: nothing
    """
    def rotate(self, matrix):
        self.process(matrix, 0)
        
    def process(self, matrix, start): 
        n = len(matrix)
        if int(n/2) <= start: 
            return
        
        for i in range(start, n-start-1):
            temp = matrix[start][i]
            matrix[start][i] = matrix[n-1-i][start]
            matrix[n-1-i][start] = matrix[n-1-start][n-1-i]
            matrix[n-1-start][n-1-i] = matrix[i][n-1-start]
            matrix[i][n-1-start] = temp
            
        self.process(matrix, start+1)
```

