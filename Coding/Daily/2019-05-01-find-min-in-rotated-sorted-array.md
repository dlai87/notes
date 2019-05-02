## Find Minimun in Rotated Sorted Array

https://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array/description

+ 二分法

+ mid单独算， 然后要缩小 range （start， mid-1） 和 （mid+1， end）

   

```python
class Solution:
    """
    @param nums: a rotated sorted array
    @return: the minimum number in the array
    """
    def findMin(self, nums):
        self.min_num = sys.maxsize
        self.binarySearch(nums, 0, len(nums)-1)
        return self.min_num
    
    def binarySearch(self, nums, start, end): 
        if start > end: 
            return 
        
        if start == end: 
            if nums[start] < self.min_num:
                self.min_num = nums[start]
            return 
        
        if nums[start] < nums[end]: 
            if nums[start] < self.min_num:
                self.min_num = nums[start]
            return 
        
        mid = int((start+end)/2)
        if nums[mid] < self.min_num:
            self.min_num = nums[mid]
        self.binarySearch(nums, start, mid-1)
        self.binarySearch(nums, mid+1, end)

```

