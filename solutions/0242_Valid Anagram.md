## 0242 Valid Anagram  
[Valid Anagram](https://leetcode.cn/problems/valid-anagram/)  

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

Input: s = "anagram", t = "nagaram"  
Output: true  

## Solutions  
- Hash  
$TC: O(n)$  单层for循环  
$SC: O(1)$  定义是的一个常量大小的辅助数组

    定义一个数组叫做record用来上记录字符串s里字符出现的次数。需要把字符映射到数组也就是哈希表的索引下标上，因为字符a到字符z的ASCII是26个连续的数值，所以字符a映射为下标0，相应的字符z映射为下标25。

    再遍历 字符串s的时候，只需要将 s[i] 所在的元素做+1 操作即可，并不需要记住字符a的ASCII，只要求出一个相对数值就可以了。 这样就将字符串s中字符出现的次数，统计出来了。

    同样在遍历字符串t的时候，对t中出现的字符映射哈希表索引上的数值再做-1的操作。

    那么最后检查一下，record数组如果有的元素不为零0，说明字符串s和t一定是谁多了字符或者谁少了字符，return false即可。

    最后如果record数组所有元素都为零0，说明字符串s和t是字母异位词，return true。

    ```python
    # Hash array
    class Solution():
        def isAnagram(self, s, t):
            record = [0] * 26
            for i in range(len(s)):
                # 标记字母的哈希表索引
                record[ord(s[i]) - ord('a')] += 1
            
            for i in range(len(t)):
                # 退回检查匹配串
                record[ord[t[i]] - ord('a')] -= 1

            for i in range(26):
                # 任何值不为0，说明多字符或者少字符
                if record[i] != 0:
                    return False
            return True

    ```

    ```python
    # Hash dict
    class Solutions():
        def isAnagram(self, s:str, t:str) -> bool:
            dict1 = {}
            for i in s:
                if i not in dict1:
                    dict1[i] = 1
                else:
                    dict1[i] += 1
            dict2 = {}
            for i in t:
                if i not in dict2:
                    dict2[i] = 1
                else:
                    dict2[i] += 1
            return dict1 == dict2
    ```
