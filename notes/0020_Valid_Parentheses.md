## 0020 Valid Parentheses

[Valid Parentheses](https://leetcode.cn/problems/valid-parentheses/)

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.

Example 1:

Input: s = "()"  
Output: true  

Example 2:

Input: s = "()[]{}"  
Output: true  

Example 3:

Input: s = "(]"  
Output: false  

## Solutions  
Use the dictionary to store the brackets.
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        mapping = {
            '(': ')',
            '[': ']',
            '{': '}'
            }
        for item in s:
            if item in mapping.keys():
                stack.append(mapping[item])
            elif not stack or stack[-1] != item:
                return False
            else:
                stack.pop()
        return True if not stack else False

```
Use list to store the brackets.

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        for item in s:
            if item == '(':
                stack.append(')')
            elif item == '[':
                stack.append(']')
            elif item == '{':
                stack.append('}')
            elif not stack or item != stack[-1]:
                return False
            else:
                stack.pop()
        return True if not stack else False
```