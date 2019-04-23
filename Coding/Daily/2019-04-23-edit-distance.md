## Edit Distance

<https://www.lintcode.com/problem/edit-distance/description>

这是二维动态规划问题。 python 的点在于 dict 里面 用[i, j] 组合作为key。而不是单个数据类型做key 

如果用 java写， 就会直接用二维数组而不是dict 

python 里上二维数组，在初始化单排或单列时候蛮头大。

```python
class Solution:
    """
    @param word1: A string
    @param word2: A string
    @return: The minimum number of steps.
    """
    def minDistance(self, word1, word2):
        m = len(word1)+1
        n = len(word2)+1
				# table 以 [i,j] 作为 key ， int 作为value
        tbl = {}
        for i in range(m): 
            tbl[i,0] = i
        for j in range(n): 
            tbl[0,j] = j
        for i in range(1, m):
            for j in range(1, n):
                cost = 0 if word1[i-1] == word2[j-1] else 1
                # 增、删、或改。 三种情况选最小的代价
                tbl[i,j] = min(tbl[i, j-1]+1, tbl[i-1, j]+1, tbl[i-1, j-1]+cost)

        return tbl[i,j]
                    
```

以下是使用二维数组的方案。 需要再熟悉一下数组的初始化。 因为python平时我数组一般不初始化指定大小的。都是动态实现。 

```python
class Solution(object):
    def minDistance(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: int
        """
        L1, L2 = len(word1), len(word2)
        # 初始化一个二维都为0的数组
        dp = [[0] * (L2 + 1) for _ in range(L1 + 1)]
        for i in range(L1 + 1):
            dp[i][0] = i
        for j in range(L2 + 1):
            dp[0][j] = j
        for i in range(1, L1 + 1):
            for j in range(1, L2 + 1):
                if word1[i - 1] == word2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
        return dp[L1][L2]

```

