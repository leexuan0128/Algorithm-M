## 0383 Ransom Note
[Ransom Note](https://leetcode.cn/problems/ransom-note/)  

Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.

Each letter in magazine can only be used once in ransomNote.

 
Example 1:

Input: ransomNote = "a", magazine = "b"  
Output: false  

Input: ransomNote = "aa", magazine = "aab" 
Output: true  

## Solutions
- Hash map  
把ransomnote中的字符和字符出现的次数存到一个key-value的map结构里。然后遍历magazine中的字符，如果存在于map里，次数减1，如果次数减到负数，那就return false，否则为true
```python
class Solutions():
    def canConstruct(self, randomNote: str, Magazine: str) -> bool:
        result = dict()
        for i in ransomNote:
            if i not in result:
                result[i] = 1
            else:
                result[i] += 1
        for j in magazine:
            if j in result and result[j] != 0:
                result[j] -= 1
        for i in result:
            if result[i] != 0:
                return False
        return True
```
