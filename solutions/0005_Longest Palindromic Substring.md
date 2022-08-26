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
$SC: O(1)$
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        for length in range(n, 0, -1):
            for i in range(n-length+1):
                if s[i:i+length] == s[i:i+length][::-1]:
                    return s[i:i+length]

```

- Center Pointer Expand

也属于左右指针的思路。具体思路是，构建一个从中心往两边扩散的函数——扩散的条件是，不超出边界且扩散的两边的元素相等，函数返回【回文字符串】。基于构建的函数，以此判断s中所有的位置，用一个res保留最长的结果。
大白话是，每个位置都判断下，以该位置为中心的回文串最长为多少，遍历一遍，保留最长的那个。
其中有一个细节，中心元素需要区分1个或者2个的情况（回文串中元素个数为奇数/偶数）
假如回文的中心为 双数，例如 abba，那么可以划分为 ab bb ba，对于n长度的字符串，这样的划分有 n-1 种。假设回文的中心为 单数，例如 abcd, 那么可以划分为 a b c d， 对于n长度的字符串，这样的划分有 n 种。对于 n 长度的字符串，我们其实不知道它的回文串中心倒底是单数还是双数，所以我们要对这两种情况都做遍历，也就是 n+(n-1) = 2n - 1，所以时间复杂度为 O(n)。

我们可以设计一个方法，兼容以上两种情况：
如果传入重合的下标，进行中心扩散，此时得到的回文子串的长度是奇数；
如果传入相邻的下标，进行中心扩散，此时得到的回文子串的长度是偶数。

$TC: O(n^2)$  
$SC: O(1)$

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ''
        # 从第一个元素一直遍历到最后一个元素，进行双向扩散
        for i in range(len(s)):
            s1 = self.expandAroundCenter(s, i, i) # 奇数串，单字符为中心进行扩散
            s2 = self.expandAroundCenter(s, i, i + 1) # 偶数串，双字符为中心进行扩散
            # 谁长谁就是这一轮的最长回文字串
            if len(s1) > len(res): 
                res = s1
            if len(s2) > len(res):
                res = s2
        return res

    def expandAroundCenter(self, s, left, right):
        # 边界条件，两边不超，左右指针所指元素相等
        while left >= 0 and right <= len(s) - 1 and s[left] == s[right]:
            left -= 1
            right += 1
        return s[left + 1: right] # 因为左指针有-1的存在，所以+1
```