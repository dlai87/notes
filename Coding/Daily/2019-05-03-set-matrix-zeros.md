## Set Matrix Zeros

https://www.lintcode.com/problem/set-matrix-zeroes/description

+ python 里面 对于一个matrix 

  rows = len(matrix) 

  cols = len(matrix[0])

  O(mn)的解法自不用多说，直接新建一个和matrix等大小的矩阵，然后一行一行的扫，只要有0，就将新建的矩阵的对应行全赋0，行扫完再扫列，然后把更新完的矩阵赋给matrix即可，这个算法的空间复杂度太高。将其优化到O(m+n)的方法是，用一个长度为m的一维数组记录各行中是否有0，用一个长度为n的一维数组记录各列中是否有0，最后直接更新matrix数组即可。这道题的要求是用O(1)的空间，那么我们就不能新建数组，我们考虑就用原数组的第一行第一列来记录各行各列是否有0.



```python
class Solution:
    """
    @param matrix: A lsit of lists of integers
    @return: nothing
    """
    def setZeroes(self, matrix):
        if not matrix:
            return
        rows = len(matrix)
        cols = len(matrix[0])
        zeroFirstCol = False 
        zeroFirstRow = False
        for i in range(rows): 
            for j in range(cols): 
                if matrix[i][j] == 0 : 
                    if i == 0 : 
                        zeroFirstRow = True
                    if j == 0 : 
                        zeroFirstCol = True
                    if i != 0 and j != 0 :
                        matrix[i][0] = 0 
                        matrix[0][j] = 0 
  
        for i in range(rows-1, 0, -1): 
            for j in range(cols-1, 0, -1):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0
        if zeroFirstRow:
            for j in range(cols):
                matrix[0][j] = 0 
        if zeroFirstCol:
            for i in range(rows):
```

