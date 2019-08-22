###Split Array into Subsequences Containing Continuous Elements

https://www.lintcode.com/problem/split-array-into-subsequences-containing-continuous-elements/description

维护两个 hashmap: 

freq —> numbers what we currently have

need—> numbers we need to meet requirement 

 

```python
class Solution:
    """
    @param nums: a list of integers
    @return: return a boolean
    """
    def isPossible(self, nums):
        freq = {}
        for num in nums:
            if num not in freq:
                freq[num] = 1 
            else:
                freq[num] += 1 

        need = {}
        for num in nums:
            if self.smartQuery(freq, num) == 0 :
                continue
            elif self.smartQuery(need, num) > 0 :
                freq = self.smartUpdate(freq, num, -1)
                need = self.smartUpdate(need, num, -1)
                need = self.smartUpdate(need, num+1, 1)
            elif self.smartQuery(freq, num+1) > 0 and self.smartQuery(freq, num+2) > 0 :
                freq = self.smartUpdate(freq, num, -1)
                freq = self.smartUpdate(freq, num+1, -1)
                freq = self.smartUpdate(freq, num+2, -1)
                need = self.smartUpdate(need, num+3, 1)
            else:
                return False
        return True 
        
    def smartUpdate(self, dict, key, value):
        if key in dict:
            dict[key] += value
        else:
            dict[key] = value 
       
        return dict 
            
    def smartQuery(self, dict, key):
        if key not in dict:
            return 0 
        return dict[key]
```

