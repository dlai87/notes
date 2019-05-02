## Combination Sum

https://www.lintcode.com/problem/combination-sum/description



```python
class Solution:
    """
    @param candidates: A list of integers
    @param target: An integer
    @return: A list of lists of integers
    """
    def DFS(self, candidates, target, start, valuelist):
        length = len(candidates)
        if target == 0:
            if valuelist not in Solution.ret:
                Solution.ret.append(valuelist)
            return 
        for i in range(start, length):
            if target < candidates[i]:
                return
            self.DFS(candidates, target - candidates[i], i, valuelist + [candidates[i]])
        
    def combinationSum(self, candidates, target):
        candidates.sort()
        Solution.ret = []
        self.DFS(candidates, target, 0, [])
        return Solution.ret
```

