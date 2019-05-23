## Longest Substring without Repeating Characters 

https://www.lintcode.com/problem/longest-substring-without-repeating-characters/my-submissions



这题主要是python 里面 queue 的实现

+ 使用collections 的 deque 
+ Queue.append  入队， queue.popleft 出队。 
+ 使用deque 的好处是可以检查一个元素是不是在 queue 里面。 

```python 
import collections 


class Solution:
    """
    @param s: a string
    @return: an integer
    """
    def lengthOfLongestSubstring(self, s):
        buf = collections.deque() 

        max_len = 0 
        for c in s: 
            if c not in buf:    # check c in queue . 
                buf.append(c)
            else: 
                while buf.popleft() != c: 
                    pass
                buf.append(c)
            max_len = max(max_len, len(buf))
        
        return max_len
```

