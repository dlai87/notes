## 1035. Rabbits in Forest

### **Description**

在一个森林中，每个兔子都有一种颜色。兔子中的一部分（也可能是全部）会告诉你有多少兔子和它们有同样的颜色。这些答案被放在了一个数组中。

返回森林中兔子可能的最少的数量。



### **Example**

**样例 1:**

```
输入: [1, 1, 2]
输出: 5
解释:
  两个回答 "1" 的兔子可能是相同的颜色，姑且说它们为红色.
  回答 "2" 的兔子一定不会是红色，不然与前面的答案冲突.
  姑且认为回答 "2" 的兔子是蓝色.
  那么一定还有 2 只蓝色的兔子在森林里不过没有回答问题.
  所以森林里兔子的最少总数是 5, 3只回答问题的加上 2 只没回答的.
```

**样例 2:**

```
输入: [10, 10, 10]
输出: 11
```



思路： 

+ 哈希表的应用

+ 数学游戏多于编程
+ 技巧性强



```python
class Solution:
    """
    @param answers: some subset of rabbits (possibly all of them) tell 
    @return: the minimum number of rabbits that could be in the forest.
    """
    def numRabbits(self, answers):
        # write your code here
        dict = {}
        for answer in answers: 
            if answer in dict: 
                dict[answer] += 1 
            else:
                dict[answer] = 1 
        total = 0 
        for key, value in dict.items(): 
            if key + 1 > value:
                total += (key + 1)
            else: 
                total += value
        return total
```





