## Group Anagrams

https://www.lintcode.com/problem/group-anagrams/description





这题的点在于, python 里面， 对string 的sort 

如果 sort('bca') 得到的是list。['a', 'b', 'c']

想要结果是'abc' 需用用  join

```python
class Solution:
    """
    @param strs: the given array of strings
    @return: The anagrams which have been divided into groups
    """
    def groupAnagrams(self, strs):
        # write your code here
        anagram_dict = {}
        for s in strs: 
            key = ''.join(sorted(s))
            if key in anagram_dict.keys():
                anagram_dict[key].append(s)
            else:
                anagram_dict[key] = [s]
        return anagram_dict.values() 
```

