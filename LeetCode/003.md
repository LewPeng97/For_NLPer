### 题目
给定一个字符串，找到最长无重复子字符串。

举例：

+ 给定的“abcabcbb”，答案是“abc”，长度为3。
+ 给定的“bbbbb”，答案是"b"，长度为1。
+ 给定的“pwwkew”，答案是"wke"，长度为3。注意是最长子字符串，不是最长子序列"pwke"。

### 思路

针对Python3语法来说，我才用两个变量进行定义，longest，value，第一个用于存储最长子字符串的长度，第二个存储无重复子串左边的起始位置。
然后创建一个哈希表，遍历整个字符串，如果字符串没有在哈希表中出现，说明没有遇到过该字符，则此时计算最长无重复子串，当且仅当哈希表中的值小于left，说明left位置更新了，此时需要重新计算最长无重复子串。每次在哈希表中将当前字符串对应的赋值加1（此方法为<font color=red>hash映射</font>）。
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        longest = 0
        left = 0
        tmp = {}
        for index, value in enumerate(s):
            if value not in tmp or tmp[value] < left:
                longest = max(longest,index-left+1)
            else:
                left = tmp[value]
            tmp[value] = index + 1
        return longest
```
