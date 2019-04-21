## Word Break 

<https://www.lintcode.com/problem/word-break/description>



    思路， DP
                            abcde  F(5)
                         /       |    |     |  \       
                bcde     cde  de   e     ""
            /  |   |  \
      cde  de e  " " 

    画解空间树， 可以看到重复的子问题。  设 F(n) 定义为， 当string还剩下n个字符时，string 是否可以wordbreak
    那么根据解空间树，可以推导递推公式   
    
    F(n)  =  str(0, 1) & F(n-1) ||  str(0, 2) & F(n-2) || .... str(0, i) & F(n-i) ... || str(0,n)  
    
```java
public boolean canWordBreak(String s, int n, List<String> wordDict, HashMap<Integer, Boolean> memo){
        if(memo.containsKey(n)){
            return memo.get(n);
        }
        int start = s.length()-n; 
        boolean res = false; 
        for(int i = 1 ; i <= n; i++){
            String subStr = s.substring(start, start+i); 
            res = res || (wordDict.contains(subStr) && memo.get(n-i));
        }
        return res; 
    }
    
    
    public boolean solutionDP(String s, List<String> wordDict){
        int N = s.length(); 
        HashMap<Integer, Boolean> memo = new HashMap<Integer, Boolean>(); 
        memo.put(0, true);
        memo.put(1, wordDict.contains(s.substring(N-1, N)));
        
        for(int i = 0 ; i <= N; i ++){
            boolean res = canWordBreak(s, i, wordDict, memo); 
            memo.put(i, res); 
        }
        return memo.get(N);
    }
    
    
    public boolean wordBreak(String s, List<String> wordDict) {
        return solutionDP(s, wordDict);
        
    }
```

以上方法虽然可以过，但是效率不高。原因在于 s.substring(start, start+i);   这个搜索的范围太广了。 其实只要索索最大的dict 里面word 的词长就够了。s.substring(start, start+max_word_length); 

改进后如下： 

```python
class Solution(object):
    """
    @param: s: A string
    @param: dict: A dictionary of words dict
    @return: A boolean
    """
    def wordBreak(self, s, dict):
        self.max_word_len = 0 
        for word in dict: 
            if len(word) > self.max_word_len: 
                self.max_word_len = len(word)
        if not dict: 
            return len(s) == 0 
        return self.dp(s, dict)
        
    def dp(self, s, dict): 
        self.memo = {}
        self.memo[0] = True
        self.memo[1] = s[-1] in dict
        
        for i in range(len(s)+1): 
            rlt = self.canWordBreak(s, i, dict)
            self.memo[i] = rlt
        return self.memo[len(s)]
        
    def canWordBreak(self, s, n, dict): 
        if n in self.memo.keys(): 
            return self.memo[n]
        start = len(s) - n 
        result= False 
        for i in range(1, min(n, self.max_word_len)+1): 
            subStr = s[start : start+i]
            result = result or ((subStr in dict) and self.memo[n-i])
        return result 
```

还可以写得简洁一些：

```python
class Solution:
    """
    @param: s: A string
    @param: dict: A dictionary of words dict
    @return: A boolean
    """
    def wordBreak(self, s, dict):
        if not dict:
            return len(s) == 0 
            
        dp = {}
        dp[0] = True
        
        len_max = 0 
        for word in dict: 
            if len(word) > len_max:
                len_max = len(word)

        for i in range(1, len(s) + 1): 
            for j in range(max(i-len_max, 0), i): 
                if dp[j] and (s[j:i] in dict):
                    dp[i] = True
                    break 
                else: 
                    dp[i] = False
                
        return dp[len(s)]
        
```

