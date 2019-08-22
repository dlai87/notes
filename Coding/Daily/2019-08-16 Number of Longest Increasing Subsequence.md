## 1093. Number of Longest Increasing Subsequence

Given an unsorted array of integers, find the number of longest increasing subsequence.

动态规划

+ 维护一个length 数组 （length[i] 表示 以 i 位字符维结尾，最长的序列长度）

+ 维护一个count 数组  (count[i] 表示 以i 位字符为结尾，最长长度为length[i] 的子序列有多少个） 

+ 两重循环，更新条件是：

  xxx, xxx, xx ,xx ,xx ,xx , xxxx, xx,xx 
                     j ——>   i 

   	1.  nums[i] > nums[j]: 
            length[i]  <  length [j] + 1 : 说明length[i] 还没有被赋值过
        	length[i] == length[j] + 1 : 说明发现新一组subseuqence  
            length[i]. > length[j] + 1 :  说明当前没有发现新的subsequence  
        	

```python
class Solution:
    """
    @param nums: an array
    @return: the number of longest increasing subsequence
    """
    def findNumberOfLIS(self, nums):
        # Write your code here
        n = len(nums)
        if n <= 0:
            return 0 
        count = [1] * n 
        length = [1] * n 
        for i in range(n):
            for j in range(i): 
                if nums[i] > nums[j] and length[j]+1 >= length[i]: 
                    if length[j]+1 == length[i]:
                        count[i] += count[j]
                    else: 
                        count[i] = count[j]
                        length[i] = length[j]+1 
        # print(count)
        # print(length)
        max_length = max(length)
        total = 0 
        for i in range(n):
            if length[i] == max_length:
                total += count[i]
        return total
```

