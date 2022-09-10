## 0541 Reverse String II  
[Reverse String II](https://leetcode.cn/problems/reverse-string-ii/)  

Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

Example 1:

Input: s = "abcdefg", k = 2  
Output: "bacdfeg"  

Example 2:  

Input: s = "abcd", k = 2  
Output: "bacd"  

## Solutions  
利用`for in`循环的特点，指定range(start, end, step)中的step为2*k
```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        temp_s = list(s)
        for i in range(0, len(temp_s), 2 * k):
            temp_s[i:i + k] = reversed(temp_s[i:i + k])
        return "".join(temp_s)
```
