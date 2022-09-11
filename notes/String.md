## Definition  
字符串是若干字符组成的有限序列，也可以理解为是一个字符数组，但是很多语言对字符串做了特殊的规定，python中字符串定义好之后是不可以原地修改的。所以我们在做题的时候，需要借助辅助字符串`temp = ''`来完成题目。  

## Python 中常用处理字符串的相关函数

- `string.capitalize()` 把字符串的第一个字符大写
- `string.count(str, beg=0, end=len(string))` 返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数
- `string.endswith(obj, beg=0, end=len(string))` 检查字符串是否以 obj 结束，如果beg 或者 end 指定则检查指定的范围内是否以 obj 结束，如果是，返回 True,否则返回 False
- `string.find(str, beg=0, end=len(string))` 检测 str 是否包含在 string 中，如果 beg 和 end 指定范围，则检查是否包含在指定范围内，如果是返回开始的索引值，否则返回-1
- `string.index(str, beg=0, end=len(string))` 跟find()方法一样，只不过如果str不在 string中会报一个异常
- `string.isalnum()` 如果 string 至少有一个字符并且所有字符都是字母或数字则返回 True,否则返回 False
- `string.isalpha()` 如果 string 至少有一个字符并且所有字符都是字母则返回 True,否则返回 False
- `string.isdecimal()` 如果 string 只包含十进制数字则返回 True 否则返回 False
- `string.isdigit()` 如果 string 只包含数字则返回 True 否则返回 False
- `string.islower()` 如果 string 中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True，否则返回 False
- `string.isnumeric()` 如果 string 中只包含数字字符，则返回 True，否则返回 False
- `string.isspace()` 如果 string 中只包含空格，则返回 True，否则返回 False
- `string.istitle()` 如果 string 是标题化的(见 title())则返回 True，否则返回 False
- `string.isupper()` 如果 string 中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True，否则返回 False
- `string.join(seq)` 以 string 作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串
- `string.lower()` 转换 string 中所有大写字符为小写
- `string.lstrip()` 截掉 string 左边的空格
- `max(str)` 返回字符串 str 中最大的字母，比较ASCII
- `min(str)` 返回字符串 str 中最小的字母，比较ASCII
- `string.replace(str1, str2, num=string.count(str1))` 把 string 中的 str1 替换成 str2,如果 num 指定，则替换不超过 num 次
- `string.split(str="", num=string.count(str))` 以 str 为分隔符切片 string，如果 num 有指定值，则仅分隔 num+ 个子字符串
- `string.startswith(obj, beg=0,end=len(string))` 检查字符串是否是以 obj 开头，是则返回 True，否则返回 False。如果beg 和 end 指定值，则在指定范围内检查.
- `string.strip([obj])` 在 string 上执行 lstrip()和 rstrip()
- `string.swapcase()` 翻转 string 中的大小写
- `string.title()` 返回"标题化"的 string,就是说所有单词都是以大写开始，其余字母均为小写(见 istitle())
- `string.translate(str, del="")` 根据 str 给出的表(包含 256 个字符)转换 string 的字符,要过滤掉的字符放到 del 参数中
- `string.upper()` 转换 string 中的小写字母为大写


## KMP  

字符串处理中一个比较著名的算法，KMP算法。KMP的主要思想是当出现字符串不匹配时，可以知道一部分之前已经匹配的文本内容，可以利用这些信息避免从头再去做匹配了。

KMP的精髓所在就是前缀表，前缀表是：起始位置到下标i之前（包括i）的子串中，有多大长度的相同前缀后缀。  
前缀：指不包含最后一个字符的所有以第一个字符开头的连续子串。  
后缀：指不包含第一个字符的所有以最后一个字符结尾的连续子串。

然后针对前缀表到底要不要减一，这其实是不同KMP实现的方式，
那么使用KMP可以解决两类经典问题：
1. 匹配问题
2. 重复子串问题

求前缀表:

```python
# 前缀表统一不减1
def getNext(next, s):
    next = next[0] * len(s)
    j = 1
    for i in range(1, len(s)):
        while j > 0 and s[i] != s[j]:
            j = next[j - 1]
        if s[i] == s[j]:
            j += 1
        next[i] = j
return next
```
