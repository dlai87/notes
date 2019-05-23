## Partition Array 

https://www.lintcode.com/problem/partition-array/description

和 quick sort 里面的 partition 部分相似

+ i 初始化使用 low - 1 的好处是，接下去 nums[i+1],nums[high] = nums[high],nums[i+1] 可以不用考虑i+1 越界问题。 如果 i 初始用 low， i + 1 有时候会越界。 需要另外处理。 
+ 各种排序算法需要再回顾

```python
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        if len(nums) == 0 :
            return 0 
        low = 0 
        high = len(nums)-1
        i = low-1        # index of smaller element  

        for j in range(low , high): 
            if   nums[j] <= k: 
                i += 1 
                nums[i],nums[j] = nums[j],nums[i] 

        nums[i+1],nums[high] = nums[high],nums[i+1] 
        
        result = 0 
        for i in range(len(nums)): 
            if nums[i] < k:
                result+=1 
                
        return result
    
```

