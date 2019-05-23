## Trapping Rain Water

https://www.lintcode.com/problem/trapping-rain-water/description



```python
class Solution:
    """
    @param heights: a list of integers
    @return: a integer
    """
    def trapRainWater(self, heights):

        left_height = []
        right_height = []
        
        max_height = 0 
        for i in range(len(heights)): 
            max_height = max(max_height, heights[i])
            left_height.append(max_height) 
        
        max_height = 0 
        for i in range(len(heights)-1, -1, -1): 
            max_height = max(max_height, heights[i])
            right_height.append(max_height) 
        right_height = right_height[::-1]
                
                
        trapping_water = 0 
        for i in range(len(heights)): 
            trapping_water += min(left_height[i], right_height[i]) - heights[i]
            
        return trapping_water

```

