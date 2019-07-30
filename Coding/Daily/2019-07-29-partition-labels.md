## Partition Labels

A string `S` of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.



### **Example**

```
Example 1:
	Input:  S = "ababcbacadefegdehijhklij"
	Output:  [9,7,8]
	
	Explanation:
	The partitions are "ababcbaca", "defegde", "hijhklij".
	A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
	
Example 2:
	Input: S = "abcab"
	Output:  [5]
	
	Explanation:
	We can not split it. 
```



思路比较直接，清晰。用了较多的python内置函数。没太考虑其它技巧性比较强的优化方案

需要总结的知识点

+ python 怎么样自定义类的sort



````python
class Solution:
    """
    @param S: a string
    @return: a list of integers representing the size of these parts
    """
    def partitionLabels(self, S):
        dict = {}
        for i in range(len(S)) : 
            c = S[i]
            if c not in dict:
                dict[c] = Range(i,i)
            else:
                dict[c].update_end(i)
        result = [] 
        for key, value in dict.items():
            if len(result) > 0 and self.has_overlap(result[-1], value): 
                result[-1] = self.merge(result[-1], value)
            else: 
                result.append(value)
            
        rlt = [] 
        index = -1 
        for r in result:
            rlt.append(r.end-index)
            index = r.end 
        return rlt 

    
    def has_overlap(self, range1, range2): 
        if (range1.start <= range2.start <= range1.end) or  (range2.start <= range1.start <= range2.end):
            return True
        return False
    
    def merge(self, range1, range2):
        return Range(min(range1.start, range2.start), max(range1.end, range2.end))
    

class Range:
    def __init__(self, start, end):
        self.start = start
        self.end = end
        
    def update_end(self, end):
        self.end = end 

    #def __str__(self):
    #    return '[{},{}]'.format(self.start, self.end)
        
````

