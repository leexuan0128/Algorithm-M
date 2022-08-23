## 0014 Longest Common Prefix
[14. Longest Common Prefix](https://leetcode.cn/problems/longest-common-prefix/)  

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".  

Example 1:  

Input: strs = ["flower","flow","flight"]  
Output: "fl"  


## Solutions:
- Max, Min of Python  
Actually, we can use `max() and min()` to compare the string in python, which compares the ASCII value of each character in the string.  
We can filter the max and min sustring in the input strs. The longest common prefix must include in those two substrings.  

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        s1 = max(strs)
        s2 = min(strs)
        for i in range(len(s1)):
            if s1[i] != s2[i]:
                return s1[:i]
        return s1
```

- Zip of Python  
Zip function can be used to extract each element in one list or unzip each element. If we use `zip(*strs)` function, we'll have`[('f', 'f', 'f'), ('l', 'l', 'l'), ('o', 'o', 'i'), ('w', 'w', 'g')]`. Obviously, the first and second index of element is the answer we want. Here we can use set() to filter the duplicate element.

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs: return ""
        ss = list(map(set, zip(*strs)))
        res = ""
        for i, x in enumerate(ss):
            x = list(x)
            if len(x) > 1:
                break
            res = res + x[0]
        return res
```