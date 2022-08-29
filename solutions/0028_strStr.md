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
