## Container With Most Water

https://www.lintcode.com/problem/container-with-most-water/description



两根指针。 

+ 两根指针算法的精髓是相向而行，使得复杂度O(n2) 降低到 O(n)

```python
class Solution:
    """
    @param heights: a vector of integers
    @return: an integer
    """
    def maxArea(self, heights):
        start = 0 
        end = len(heights)-1 
        max_water = 0 
        while start < end : 
            current = (end-start) * min(heights[start], heights[end])
            max_water = max(max_water , current)
            if heights[start] < heights[end]:
                start += 1 
            else: 
                end -= 1
        return max_water
```

