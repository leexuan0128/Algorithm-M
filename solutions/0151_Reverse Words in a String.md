## 0151 Reverse Words in a String  
[Reverse Words in a String](https://leetcode.cn/problems/reverse-words-in-a-string/)  

Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

 

Example 1:

Input: s = "the sky is blue"  
Output: "blue is sky the"  

Example 2:

Input: s = "  hello world  "  
Output: "world hello"  
Explanation: Your reversed string should not contain leading or trailing spaces.

Example 3:  

Input: s = "a good   example"  
Output: "example good a"  
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.


## Solutions  
```python
class Solution:
    def reverseWords(self, s: str) --> str:
        return " ".join(s.split().reverse())

```

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        s = self.remove_spaces(s)
        s = self.reverse_string(s)
        s = self.reverse_each_word(s)

        return "".join(s)

    # remove extra spaces
    def remove_spaces(self, s):
        # initialize the two pointers
        left, right = 0, len(s)-1
        # remove front spaces
        while (left < right) and s[left] == " ":
            left += 1
        # remove tailing spaces
        while (left < right) and s[right] == " ":
            right -= 1
        # build a new array to store left elements
        new_s = []
        # remove extra in-line spaces
        while (left <= right):
            if(s[left] != " "):
                new_s.append(s[left])
            elif (s[left] == " " and new_s[-1] != " "):
                new_s.append(s[left])
            left += 1
        
        return new_s

    def reverse_string(self, s):
        left, right = 0, len(s)-1
        while (left < right):
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
        
        return s

    def reverse_each_word(self, s):
        left, right = 0, 0
        n = len(s)
        while (left < n):
            while (right < n) and s[right] != " ":
                right += 1
            s[left:right] = self.reverse_string(s[left:right])
            left = right + 1
            right += 1
            
        return s
```