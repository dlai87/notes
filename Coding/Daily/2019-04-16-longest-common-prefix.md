## LintCode 78 

<https://www.lintcode.com/problem/longest-common-prefix/description>

### **Description**

Given k strings, find the longest common prefix (*LCP*).



Idea: Trie Tree 

```python
class Solution:
    """
    @param strs: A list of strings
    @return: The longest common prefix
    """
    
  
    def longestCommonPrefix(self, strs):
        # edge case 
        if strs == None or len(strs) == 0 : 
            return ""
        # build trie tree 
        root = TrieNode('')
        for string in strs: 
            # edge case 2 
            if len(string) == 0:
                return ""
            self.addString(root, string)
            
        # search the trie tree 
        index = 0 
        current_node = root
        while len(current_node.children) == 1 : 
            index += 1 
            for key, value in current_node.children.items(): 
                current_node = value
                
        # get result 
        return strs[0][0:index]
        
    def addString(self, root, string): 
        current_node = root
        for c in string: 
            if c in current_node.children: 
                current_node = current_node.children[c]
            else: 
                temp = TrieNode(c)
                current_node.children[c] = temp
                current_node = temp
        
class TrieNode: 
    
    def __init__(self, char): 
        self.char = char
        self.children = {}

```

+ There shoulde be none-trie-tree solutions too.  I just use something I am comfortable with. 
+ Edge cases should be considered while using trie tree. 
+ Trie is a little "Over Kill"

