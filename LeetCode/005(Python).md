### 题目

给定一个字符串 `s`，找到 `s` 中最长的回文子串。你可以假设 `s` 的最大长度为 1000。

**示例1**

```
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
```

**示例 2：**

```
输入: "cbbd"
输出: "bb"
```

### 思路

```
中心扩展法
```

### 代码

```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def expand(i,j,s):
            while(i>=0 and j<len(s) and s[i] == s[j]):
                i -= 1
                j += 1
            return s[i+1:j]
        if len(s) == 0:
            return ""
        longest = s[0]
        for i in range(len(s)):
            str1 = expand(i,i,s)
            str2 = expand(i,i+1,s)
            if max(len(str1),len(str2)) > len(longest):
                longest = str1 if len(str1) > len(str2) else str2
        return longest
```

