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

- Center Pointer

也属于左右指针的思路。具体思路是，构建一个【从中心往两边扩散】的函数——扩散的条件是，不超出边界且扩散的两边的元素相等，函数返回【回文字符串】。基于构建的函数，以此判断s中所有的位置，用一个res保留最长的结果。
大白话是，每个位置都判断下，以该位置为中心的回文串最长为多少，遍历一遍，保留最长的那个。
其中有一个细节，中心元素需要区分1个或者2个的情况（回文串中元素个数为奇数/偶数）

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def palindrome(s, l, r):
            while l >= 0 and r < len(s) and s[l] == s[r]:
                l -= 1
                r += 1
            return s[l+1:r]
        
        res = ''
        for i in range(len(s)):
            sub1 = palindrome(s, i, i)
            sub2 = palindrome(s, i, i+1)
            res = sub1 if len(sub1) > len(res) else res
            res = sub2 if len(sub2) > len(res) else res
        return res
```