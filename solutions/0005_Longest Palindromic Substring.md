## 0005 Longest Palindromic Substring
[Longest Palindromic Substring](https://leetcode.cn/problems/longest-palindromic-substring/)  

Given a string s, return the longest palindromic substring in s.  

Example 1:

Input: s = "babad"  
Output: "bab"  
Explanation: "aba" is also a valid answer.  

## Solutions
- Brute Force  
$TC: O(n^3)$  
$SC: O(n)$
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        for length in range(n, 0, -1):
            for i in range(n-length+1):
                if s[i:i+length] == s[i:i+length][::-1]:
                    return s[i:i+length]

```
