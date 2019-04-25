## Longest Consecutive Sequence

<https://www.lintcode.com/problem/longest-consecutive-sequence/description>



这题点在于，对于已经搜索过的数，避免重复搜索。

+ 我的做法是利用python set 的一些操作，在搜索临近数字时候，如果数字在set 中，及时清理掉。这样可以避免重复搜索。 

+ 由于set 的大小在动态变化，不适合使用for loop，所以使用while 循环， 检查set是否为空
+ Set.pop 随便弹出一个数，（并从set 中删除）
+ set.remove(element) 移除某个元素

```python
class Solution:
    """
    @param num: A list of integers
    @return: An integer
    """
    def longestConsecutive(self, num):
        self.max_len = 0 
        self.num_set = set(num)
        while self.num_set:
            n = self.num_set.pop()
            self.get_consecutive_len(n)
        return self.max_len
            
    def get_consecutive_len(self, n): 
        temp_max = 1
        pre = n-1 
        while pre in self.num_set: 
            temp_max += 1 
            self.num_set.remove(pre)
            pre -= 1 
        post = n+1 
        while post in self.num_set: 
            temp_max += 1 
            self.num_set.remove(post)
            post += 1 
        self.max_len = max(self.max_len, temp_max)
        
```

