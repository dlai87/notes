## Max points on a line

https://www.lintcode.com/problem/max-points-on-a-line/description

算斜率， 用hash表保存每个斜率下的点。由于只需要计算有多少点，所以存点的个数就够了

两个特殊情况:

+ 两个点重合    用 samepoint 变量解决

+ 斜率垂直       用 inf 斜率解决

  注： slope 斜率表在第一层初始化，而不是在最外层。这样可以避免很多麻烦。 samepoint 这个变量就是和斜率表都是只针对 point1 的。 count变量在最外层，count 针对全局。

```python
"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""

class Solution:
    """
    @param points: an array of point
    @return: An integer
    """
    def maxPoints(self, points):
        if not points:
            return 0 
        if len(points) < 2 : 
            return len(points)
        
        count = 0 # count 在最外层全局
        for i in range(len(points)-1):
            point1 = points[i]
            samapoint = 1 # the point itself is 1 
            slope = {'infinit': 0}  # 斜率在这一层初始化，而不是在最外层。
            for j in range(i+1, len(points)): 
                point2 = points[j]
                if point1.x == point2.x:
                    if point1.y == point2.y: 
                        samapoint += 1 
                    else:
                        slope['infinit'] += 1
                else:
                    k = str ( (point1.y - point2.y) / (point1.x - point2.x))
                    if k not in slope.keys():
                        slope[k] = 1
                    else:
                        slope[k] += 1
            count = max(count, max(slope.values())+samapoint )        
        return count 
                
```

