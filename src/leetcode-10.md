# leetcode-algorithms-10 Regular Expression Matching

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.
```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```
The matching should cover the entire input string (not partial).

Note:

+ s could be empty and contains only lowercase letters a-z.
+ p could be empty and contains only lowercase letters a-z, and characters like . or *.

Example 1:
```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

Example 2:
```
Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

Example 3:
```
Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

Example 4:
```
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".
```

Example 5:
```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

## 解法1

```
class Solution
{
public:
    bool isMatch(string s, string p)
    {
        if (p.empty()) return s.empty();
        
        //检查首字母是否匹配,因为'*'通配符要有前置元素,所以不需要考虑
        bool match = (!s.empty() && (p[0] == s[0] || p[0] == '.'));
        
        if (p.size() >= 2 && p[1] == '*')
            //第二个字母为'*',这有2种情况,'*'号为0时和'*'号不为0时
            return (isMatch(s, p.substr(2)) || (match && isMatch(s.substr(1), p))); 
        else
            //第二个字母不为'*'继续.
            return match && isMatch(s.substr(1), p.substr(1));

        return false;         
    }
};
```

时间复杂度: O(min(n, m)).

空间复杂度: O(1).


## 解法2

利用C++11 regex正规库
```
class Solution
{
public:
    bool isMatch(string s, string p)
    {
        return std::regex_match(s, std::regex(p));
    }
};
```