## 0028 Implementing strStr()
[Implementing strStr()](https://leetcode.cn/problems/implement-strstr/)  

Implement strStr().

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

Example 1:

Input: haystack = "hello", needle = "ll"  
Output: 2  

## Solutions  
- Brute Force  
$SC: O(m*n)$ m is the length of the substring while n is the length of the origin string  
$TC: O(1)$  we only need constant space to save variants  

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        # null -> 0
        if not needle: return 0
        m, n = len(needle), len(haystack)
        # if m > n -> -1
        if m > n: return -1
        # comparison one by one
        for i in range(n - m + 1):
            if haystack[i: i + m] == needle:
                return i
        return -1
```
- KMP  
$SC: O(m+n)$  n 为原串的长度，m 为匹配串的长度。  
$TC: O(m)$  
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle: return 0
        n, m = len(haystack), len(needle)
        # 原串和匹配串前面都加空格，使其下标从 1 开始
        haystack = " " + haystack
        needle = " " + needle
        next = self.get_next(m, needle)
        # 匹配过程，i = 1，j = 0 开始，i 小于等于原串长度
        i, j = 1, 0 
        while i <= n:
            # 匹配不成功的话，j = next(j)
            while j > 0 and haystack[i] != needle[j + 1]:
                j = next[j]
            # # 匹配成功的话，先让 j++
            if haystack[i] == needle[j + 1]:
                j += 1
            # 整一段匹配成功，直接返回下标
            if j == m:
                return i - m
            i += 1
        return -1

    def get_next(self, m, needle):
        # 构造过程 i = 2，j = 0 开始，i 小于等于匹配串长度
        next = [0] * (m + 1)
        i, j = 2, 0
        while i <= m:
            # 匹配不成功的话，j = next(j)
            while j > 0 and needle[i] != needle[j + 1]:
                j = next[j]
            # 匹配成功的话，先让 j++
            if needle[i] == needle[j + 1]:
                j += 1
            # 更新 next[i], i++, 结束本次循环
            next[i] = j
            i += 1
        return next
```